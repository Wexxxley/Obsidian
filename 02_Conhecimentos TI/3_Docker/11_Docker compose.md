
#Concluded 

---
### **1. O que é docker compose**

Aplicações reais são sistemas distribuídos: uma API, um site front-end, um banco de dados, um cache Redis, etc. Se você tivesse que rodar tudo isso manualmente, teria que digitar comandos gigantes e gerenciar volumes na mão. 

O **Docker Compose** resolve isso. Ele permite que você escreva um único arquivo descrevendo toda a sua aplicação e a inicie com um único comando.

Para entender o Compose, você precisa entender a mudança de mentalidade:

1. **Imperativo (Scripts):**
    - Você diz o que fazer passo a passo.        
    - Problema: Se você rodar o script duas vezes, ele pode criar contêineres duplicados ou dar erro porque a rede já existe.
        
2. **Declarativo (Docker Compose):**
    - Você diz qual deve ser o resultado final: "Eu quero um sistema que tenha: 1 serviço web na porta 80 e 1 banco de dados".
    - Você entrega esse "mapa" para o Docker Compose. Ele olha para o que já está rodando, compara com o mapa e decide o que precisa criar ou atualizar.

---
### **2. O arquivo docker-compose.yml**

O "mapa" da sua aplicação é escrito em um arquivo chamado `docker-compose.yml`. A sintaxe é simples e legível.

Vamos analisar um exemplo para a aplicação To-Do List.

```
version: '3.7'  # Versão Compose

services:       
  todo-web:     # Nome do primeiro serviço
    image: diamol/ch06-todo-list
    ports:
      - "8020:80" # Mapeia porta 8020 do PC para 80 do container    
    networks:
      - app-net     

  todo-db:      # Nome do segundo serviço 
    image: diamol/postgres:11.5
    ports:
      - "5433:5432"
    networks:
      - app-net      
        
networks:       # Definição das redes
  app-net:      
    external:
      name: nat 
```

**O que esse arquivo diz?**
> "Docker, eu quero dois serviços: um site e um banco. Quero que ambos estejam na rede app-net para poderem conversar entre si. O site deve estar acessível para mim na porta 8020."


---
### **3. Gerenciando a aplicação**

**Iniciando a aplicação inteira:**    
- `docker-compose up -d`
- `up`: Cria e inicia tudo o que está no arquivo.
- `-d`: Roda em segundo plano.

**Verificando status:** 
- `docker-compose ps`
- Isso mostra apenas os contêineres deste projeto, ignorando outros contêineres do seu sistema.

**Parando containers:**
- `docker-compose stop`
- Só para os containers

**Para parar e remover TUDO:**
- `docker-compose down`    
- Deleta os contêineres. Remove a rede que foi criada para eles se comunicarem.
- Mas mantem a imagem e os volumes.