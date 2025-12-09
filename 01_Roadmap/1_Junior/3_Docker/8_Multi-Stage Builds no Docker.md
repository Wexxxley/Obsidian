

---
No desenvolvimento de software tradicional, existe um processo rigoroso e muitas vezes doloroso. O código vai para um repositório central e um **servidor de build** precisa baixar o código, compilar e gerar o executável.

- Eles precisam ter **todas** as ferramentas instaladas e atualizadas (Java JDK, .NET SDK, Node.js, Python, Make, GCC, etc.).
    
- As versões das ferramentas no servidor de build precisam ser **idênticas** às do computador do desenvolvedor.

Com o Docker, você empacota o próprio conjunto de ferramentas de build dentro de uma imagem.

A técnica de **Multi-Stage Build** divide o processo em duas fases lógicas dentro do mesmo arquivo:

1. **Estágio 1 (Builder):**
    - Usa uma imagem base pesada (SDKs, Compiladores).
    - Baixa dependências, compila código fonte.
    - Gera o artefato final (o binário ou o ambiente virtual).
        
2. **Estágio 2 (Final):**
    - Usa uma imagem base leve (o mínimo necessário para rodar o app).
    - Copia apenas o artefato gerado no Estágio 1.
    - O resto do "entulho" (código fonte original, caches do gerenciador de pacotes, compiladores) é destruído junto com o Estágio 1.

---
### **1. Exemplo: Python (Interpretado)**

Linguagens interpretadas como Python não geram um binário único, mas podemos isolar as dependências em um ambiente virtual para manter a imagem final limpa.

**Dockerfile**
```Dockerfile
# ==========================================
# ESTÁGIO 1: Builder

FROM python:3.9 AS builder # Dando nome ao estagio

WORKDIR /app # Diretorio de trabalho
 
RUN python -m venv /opt/venv # Cria um ambiente virtual para isolar as bibliotecas
# Ativa o venv para os próximos comandos
ENV PATH="/opt/venv/bin:$PATH"

COPY requirements.txt .
# Instala as libs dentro do venv
RUN pip install --no-cache-dir -r requirements.txt

# ==========================================
# ESTÁGIO 2: A Imagem Final (Produção)
# ==========================================
FROM python:3.9-slim

WORKDIR /app

# A MÁGICA: Copiamos APENAS a pasta do ambiente virtual do estágio 'builder'
# Todo o resto (compiladores, caches, logs) fica para trás.
COPY --from=builder /opt/venv /opt/venv

# Adicionamos o venv ao PATH desta nova imagem para que o comando python/uvicorn funcione
ENV PATH="/opt/venv/bin:$PATH"

# Copiamos apenas o código da aplicação
COPY main.py .

# Comando para rodar o servidor
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "80"]
```

---

### 4. Exemplo Prático 2: .NET (Compilado)

Este exemplo demonstra a economia brutal de espaço. O SDK do .NET é enorme (cerca de 800MB), mas o Runtime (apenas para rodar o app) é pequeno (cerca de 200MB).

Imagine uma API simples em C#.

**Arquivo:** `Program.cs`

C#

```
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/", () => "Docker com .NET é vida!");

app.Run();
```

**Dockerfile:**

Dockerfile

```
# ==========================================
# ESTÁGIO 1: Build (O SDK Pesado)
# Usamos a imagem SDK que contém o compilador 'dotnet build'
# ==========================================
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /src

# Copia o arquivo de projeto e restaura dependências
COPY MeuProjeto.csproj .
RUN dotnet restore

# Copia todo o resto do código e compila uma versão de lançamento (Release)
COPY . .
# O comando 'publish' gera os arquivos DLL finais na pasta /app/publish
RUN dotnet publish -c Release -o /app/publish

# ==========================================
# ESTÁGIO 2: Runtime (A Imagem Leve)
# Note que usamos 'aspnet', não 'sdk'. Esta imagem NÃO tem compilador.
# ==========================================
FROM mcr.microsoft.com/dotnet/aspnet:8.0

WORKDIR /app

# A MÁGICA: Copiamos apenas os arquivos compilados (DLLs) do estágio anterior.
# O código fonte C# (que não serve pra nada em produção) é descartado.
COPY --from=build /app/publish .

# Define o comando de entrada
ENTRYPOINT ["dotnet", "MeuProjeto.dll"]
```

**O que acontece aqui?**

1. **No Estágio `build`:** O Docker baixa a imagem SDK (~800MB), baixa pacotes NuGet e compila o código C# em arquivos DLL.
    
2. **No Estágio Final:** O Docker inicia uma imagem ASP.NET limpa (~200MB).
    
3. **A Cópia:** Ele pega apenas as DLLs da pasta `/app/publish`.
    
4. **O Resultado:** Você tem um contêiner de produção super leve e seguro, pois não contém o código fonte original nem ferramentas capazes de recompilar código (o que dificulta a vida de hackers).
    

---

### 5. Resumo dos Benefícios

1. **Tamanho:** Imagens finais drasticamente menores (economiza disco e banda de rede).
    
2. **Segurança:** A imagem de produção não tem código fonte, gerenciadores de pacotes (como `apt` ou `apk` desnecessários) ou compiladores.
    
3. **Padronização:** Qualquer pessoa, em qualquer OS, pode gerar o binário da aplicação apenas tendo o Docker instalado, sem poluir seu computador com SDKs.