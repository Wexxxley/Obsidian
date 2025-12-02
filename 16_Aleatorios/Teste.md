
---

### Fase 1: Docker
O objetivo é fazer o projeto rodar antes de escrever código Python. O projeto django vai ficar encapsulad em um container e o db em outro.

**1. Crie os arquivos na raiz do projeto**

**Arquivo: `requirements.txt`**
```
django
djangorestframework
psycopg2-binary
pillow
python-dotenv
drf-spectacular
```

**Arquivo: `Dockerfile`**
```
FROM python:3.10-slim
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
WORKDIR /app
# Instala dependências do sistema para o Postgres
RUN apt-get update && apt-get install -y libpq-dev gcc
# Instala Python libs
COPY requirements.txt /app/
RUN pip install --upgrade pip && pip install -r requirements.txt
COPY . /app/
```

**Arquivo: `docker-compose.yml`**

```
version: '3.8'

services:
  db:
    image: postgres:15-alpine
    environment:
      - POSTGRES_DB=teste_db
      - POSTGRES_USER=user_teste
      - POSTGRES_PASSWORD=senha_segura
    volumes:
      - postgres_data:/var/lib/postgresql/data

  web:
    build: .
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/app
    ports:
      - "8000:8000"
    depends_on:
      - db
    environment:
      - DB_NAME=teste_db
      - DB_USER=user_teste
      - DB_PASSWORD=senha_segura
      - DB_HOST=db
      - DB_PORT=5432

volumes:
  postgres_data:
```

**2. Subir o ambiente:**

```
sudo docker-compose up -d --build
```

_(Se der erro de permissão, use `sudo chown -R $USER:$USER .`)_

---
### Fase 2: Configuração do Django

O objetivo é conectar o Django ao Postgres e instalar libs.

**Edite `store_api/settings.py`:**

1. **Imports:** Adicione `import os` no topo.
    
2. **Apps:** Atualize `INSTALLED_APPS` 2:
        
    ```
    INSTALLED_APPS = [
        # ... apps nativos ...
        'rest_framework',
        'drf_spectacular',
        'api', 
    ]
    ```

ALLOWED_HOSTS = ['*']

1. **Banco de Dados:** Atualize `DATABASES` para ler do Docker 3:
    ```
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.postgresql',
            'NAME': os.environ.get('DB_NAME', 'teste_db'),
            'USER': os.environ.get('DB_USER', 'user_teste'),
            'PASSWORD': os.environ.get('DB_PASSWORD', 'senha_segura'),
            'HOST': os.environ.get('DB_HOST', 'db'),
            'PORT': os.environ.get('DB_PORT', '5432'),
        }
    }
    ```
    
2. **Swagger:** Adicione no final do arquivo:
    
    ```
    REST_FRAMEWORK = {
        'DEFAULT_SCHEMA_CLASS': 'drf_spectacular.openapi.AutoSchema',
    }
    SPECTACULAR_SETTINGS = {
        'TITLE': 'Catálogo de Produtos API',
        'DESCRIPTION': 'API do Desafio Técnico',
        'VERSION': '1.0.0',
    }
    MEDIA_URL = '/media/'
    MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
    ```
    


---

### Fase 3: Modelagem de Dados

O objetivo é criar as tabelas no banco.

**Arquivo: `api/models.py`** 

```python
from django.db import models

class Category(models.Model):
    name = models.CharField(max_length=100)
    class Meta:
        verbose_name_plural = "Categories"
    def __str__(self):
        return self.name

class Product(models.Model):
    name = models.CharField(max_length=100)
    description = models.TextField()
    price = models.DecimalField(max_digits=10, decimal_places=2)
    # Requisito: Proteção ao deletar categoria pai
    category = models.ForeignKey(Category, on_delete=models.PROTECT, related_name='products')
    # Bônus: Upload de imagem
    image = models.ImageField(upload_to='products/', null=True, blank=True)

    def __str__(self):
        return self.name
```

**Rode as Migrações:**
```
sudo docker-compose exec web python manage.py makemigrations
sudo docker-compose exec web python manage.py migrate

sudo docker-compose exec web python manage.py createsuperuser
```

---

### Fase 4: API e Serializers

Objetivo: Criar a lógica de entrada e saída de dados.

**Arquivo: `api/serializers.py` (Crie este arquivo)**

```
from rest_framework import serializers
from .models import Category, Product

class CategorySerializer(serializers.ModelSerializer):
    class Meta:
        model = Category
        fields = '__all__'

class ProductSerializer(serializers.ModelSerializer):
    # Truque: Mostra o nome na leitura, mas pede ID na escrita
    category_name = serializers.CharField(source='category.name', read_only=True)

    class Meta:
        model = Product
        fields = ['id', 'name', 'description', 'price', 'category', 'category_name', 'image']
```

**Arquivo: `api/views.py`**

```
from rest_framework import viewsets
from rest_framework.parsers import MultiPartParser, FormParser
from drf_spectacular.utils import extend_schema
from .models import Category, Product
from .serializers import CategorySerializer, ProductSerializer

class CategoryViewSet(viewsets.ModelViewSet):
    queryset = Category.objects.all()
    serializer_class = CategorySerializer

class ProductViewSet(viewsets.ModelViewSet):
    queryset = Product.objects.all()
    serializer_class = ProductSerializer
    # 1. Habilita o suporte a upload de arquivos
    parser_classes = (MultiPartParser, FormParser)

    # 2. Força o Swagger a desenhar o botão de arquivo
    @extend_schema(
        operation_id='create_product',
        request={
            'multipart/form-data': {
                'type': 'object',
                'properties': {
                    'name': {'type': 'string'},
                    'description': {'type': 'string'},
                    'price': {'type': 'number'},
                    'category': {'type': 'integer'},
                    'image': {'type': 'string', 'format': 'binary'}, 
                },
                'required': ['name', 'description', 'price', 'category']
            }
        }
    )
    def create(self, request, *args, **kwargs):
        """
        Cria um novo produto com upload de imagem.
        """
        return super().create(request, *args, **kwargs)
```

---

### Fase 5: Rotas (URLs)

_Objetivo: Ligar tudo na internet._

**Arquivo: `store_api/urls.py`**

```
from django.contrib import admin
from django.urls import path, include
from django.conf import settings
from django.conf.urls.static import static
from rest_framework.routers import DefaultRouter
from drf_spectacular.views import SpectacularAPIView, SpectacularSwaggerView
from api.views import CategoryViewSet, ProductViewSet

router = DefaultRouter()
router.register(r'categories', CategoryViewSet)
router.register(r'products', ProductViewSet)

urlpatterns = [
    path('admin/', admin.site.urls),
    path('api/', include(router.urls)),
    # Swagger Docs
    path('api/schema/', SpectacularAPIView.as_view(), name='schema'),
    path('api/docs/', SpectacularSwaggerView.as_view(url_name='schema'), name='swagger-ui'),
]

if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

![](../attachments/Pasted%20image%2020251202081852.png)

---

### ✅ Fase 6: Testar

1. **Acesse:** `http://127.0.0.1:8000/api/docs/`

Se der erro:
sudo docker-compose down
sudo docker-compose build --no-cache
sudo docker-compose up -d
sudo docker-compose exec web python manage.py makemigrations
sudo docker-compose exec web python manage.py migrate


2. **Crie uma Categoria** (POST).
    
3. **Crie um Produto** (POST) usando o ID da categoria criada e enviando uma imagem.

---

# api/admin.py


```python
from django.contrib import admin
from .models import Category, Product 
  
@admin.register(Category)
class CategoryAdmin(admin.ModelAdmin):
	list_display = ('id', 'name') 

@admin.register(Product)
class ProductAdmin(admin.ModelAdmin):
	list_display = ('name', 'price', 'category')
	list_filter = ('category',) 
	search_fields = ('name',) 
```

http://127.0.0.1:8000/admin/