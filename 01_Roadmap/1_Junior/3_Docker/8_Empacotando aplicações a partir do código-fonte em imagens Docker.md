


---
No desenvolvimento de software tradicional, existe um processo rigoroso. O código vai para um repositório central e um servidor de build baixa o código, compila e gera o executável. Manter servidores de build é difícil.

- Eles precisam ter **todas** as ferramentas instaladas (Java, .NET, Node, etc.).
- As versões das ferramentas no servidor de build precisam ser idênticas às do seu computador, senão o build falha.

Com docker você pode empacotar o próprio conjunto de ferramentas de build em uma imagem Docker.
- Você escreve um Dockerfile que usa uma imagem com as ferramentas de compilação.
- O Docker compila seu código dentro desse contêiner.
- O resultado final é o seu aplicativo empacotado.    

Isso elimina a necessidade de instalar ferramentas no seu PC ou no servidor. Só o Docker é necessário.

1. **Estágio 1 (Build):** Usa uma imagem pesada com todas as ferramentas (compiladores, SDKs). Compila o código e gera o binário.
    
2. **Estágio 2 (Final):** Usa uma imagem leve (só o runtime). Copia **apenas** o binário gerado no Estágio 1. O resto do lixo (código fonte, compiladores) é descartado.

### O Exemplo Prático: FastAPI

Vamos criar uma API simples. 

main.py
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Mensagem": "Múltiplos estágios funcionam!"}
```

**requirements.txt**
```
fastapi
uvicorn
```

**Dockerfile**
Aqui está o segredo. Vamos dividir o Dockerfile em dois blocos `FROM`.

```Dockerfile
# ==========================================
# ESTÁGIO 1: Builder

FROM python:3.9 AS builder # Dando nome ao estágio

WORKDIR /app # Diretorio de trabalho

RUN python -m venv /opt/venv # Cria um ambiente virtual

ENV PATH="/opt/venv/bin:$PATH" # Ativa o venv para próximos comandos

COPY requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# ==========================================
# ESTÁGIO 2: A Imagem Final (Produção)

FROM python:3.9-slim

WORKDIR /app # Define o diretório de trabalho na imagem final

# Copiamos APENAS a pasta do ambiente virtual de 'Builder'
# Todo o resto (caches, compiladores, logs do pip) fica para trás.

COPY --from=builder /opt/venv /opt/venv

# Adicionamos o venv ao PATH desta nova imagem
ENV PATH="/opt/venv/bin:$PATH"

# Copiamos o código da aplicação
COPY main.py .

# Comando para rodar o servidor
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "80"]
```

1. **No Estágio `builder`:** Nós baixamos uma imagem Python completa. Criamos um ambiente virtual e instalamos o FastAPI e o Uvicorn dentro dele. Essa imagem ficou "suja" e pesada.
    
2. **No Estágio Final:** O Docker iniciou uma nova imagem limpa.
    
3. **A Cópia (`COPY --from=builder`):** Nós pegamso apenas a pasta `/opt/venv` (onde as bibliotecas foram instaladas) do primeiro estágio e jogamos no segundo.
    
4. **O Resultado:** O Estágio 1 é descartado. Sua imagem final tem apenas o Linux básico, o Python e as pastas do seu projeto.
