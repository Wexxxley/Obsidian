


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

```Dockerfile
FROM diamol/base:2e AS build-stage
RUN echo 'Building...' > /build.txt

FROM diamol/base:2e AS test-stage
COPY --from=build-stage /build.txt /build.txt
RUN echo 'Testing...' >> /build.txt

FROM diamol/base:2e
COPY --from=test-stage /build.txt /build.txt
CMD ["cat", "/build.txt"]
```


- **`AS nome-estagio`**: Dá um apelido para aquela etapa.
- **`COPY --from=...`**: Essa é a mágica. Em vez de copiar do seu computador, ele copia um arquivo de um estágio anterior para o atual.
    
- **`RUN`**: Executa um comando dentro do contêiner durante o build (aqui, apenas criando um arquivo de texto para simular uma compilação).
    

O resultado final é uma imagem única contendo apenas o que está no último estágio (`FROM`), mas que carrega o resultado dos estágios anteriores.

#### Tente agora: Construindo com múltiplos estágios

Vamos ver isso na prática com o exemplo simples acima.

1. Navegue para a pasta do exercício: `cd ch04/exercises/multi-stage`
    
2. Construa a imagem: `docker image build -t multi-stage .`
    

Observe a saída. Você verá o Docker executando cada estágio sequencialmente (`Step 1/x : FROM...`, `Step x/x : RUN...`).

---

### 4.2 Passo a passo do App: Código-fonte Java

Agora vamos para um exemplo do mundo real. Vamos construir uma aplicação **Java Spring Boot**.

**Nota importante:** Você **não** precisa ter Java ou Maven instalados na sua máquina. O Docker vai baixar tudo o que precisa.

O código está em `ch04/exercises/image-of-the-day`. Ele usa **Maven** (ferramenta de build) e **OpenJDK** (kit de desenvolvimento Java).

A **Listagem 4.2** mostra o Dockerfile para esse app:

Dockerfile

```
FROM diamol/maven:2e AS builder
WORKDIR /usr/src/iotd
COPY pom.xml .
RUN mvn -B dependency:go-offline
COPY . .
RUN mvn package

# app
FROM diamol/openjdk:2e
WORKDIR /app
COPY --from=builder /usr/src/iotd/target/iotd-service-0.1.0.jar .
EXPOSE 80
ENTRYPOINT ["java", "-jar", "/app/iotd-service-0.1.0.jar"]
```
