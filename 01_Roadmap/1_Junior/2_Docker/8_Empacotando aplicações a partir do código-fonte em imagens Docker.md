


---
Você aprendeu que precisa apenas de algumas instruções em um Dockerfile para empacotar um aplicativo. Mas há mais uma coisa que você precisa saber para empacotar seus próprios aplicativos: você também pode **rodar comandos** dentro dos Dockerfiles.

Comandos executados durante o build salvam as alterações do sistema de arquivos na camada da imagem. Isso torna os Dockerfiles o formato de empacotamento mais flexível que existe; você pode descompactar arquivos, rodar instaladores e fazer praticamente qualquer coisa.

### 4.1 Quem precisa de um servidor de build quando você tem um Dockerfile?

No desenvolvimento de software tradicional, existe um processo rigoroso. O código vai para um repositório central e um servidor de build baixa o código, compila e gera o executável. Manter servidores de build é difícil.

- Eles precisam ter **todas** as ferramentas instaladas (Java, .NET, Node, etc.).
- As versões das ferramentas no servidor de build precisam ser idênticas às do seu computador, senão o build falha.
    
- A **Figura 4.1** do livro ilustra essa complexidade: todos precisam ter o mesmo conjunto de ferramentas .
    

**A Solução Docker:** Você pode empacotar o próprio conjunto de ferramentas de build em uma imagem Docker.

- Você escreve um Dockerfile que usa uma imagem com as ferramentas de compilação.
    
- O Docker compila seu código dentro desse contêiner.
    
- O resultado final é o seu aplicativo empacotado.
    

Isso elimina a necessidade de instalar ferramentas no seu PC ou no servidor. Só o Docker é necessário.

#### Entendendo Dockerfiles de Múltiplos Estágios (Multi-stage)

Para fazer isso de forma eficiente, usamos **múltiplos estágios**.

1. **Estágio 1 (Build):** Usa uma imagem pesada com todas as ferramentas (compiladores, SDKs). Compila o código e gera o binário.
    
2. **Estágio 2 (Final):** Usa uma imagem leve (só o runtime). Copia **apenas** o binário gerado no Estágio 1. O resto do lixo (código fonte, compiladores) é descartado.
    

A **Listagem 4.1** mostra um exemplo básico desse fluxo :

Dockerfile

```
FROM diamol/base:2e AS build-stage
RUN echo 'Building...' > /build.txt

FROM diamol/base:2e AS test-stage
COPY --from=build-stage /build.txt /build.txt
RUN echo 'Testing...' >> /build.txt

FROM diamol/base:2e
COPY --from=test-stage /build.txt /build.txt
CMD ["cat", "/build.txt"]
```

**Análise do Script:**

- **`AS nome-do-estagio`**: Dá um apelido para aquela etapa (ex: `build-stage`).
    
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

**O que está acontecendo aqui?**

1. **Estágio `builder`:**
    
    - Usa a imagem `diamol/maven`. Ela é grande e tem todas as ferramentas para compilar Java.
        
    - `COPY pom.xml .` e `RUN mvn ...`: Copia o arquivo de dependências e as baixa da internet. Isso é feito antes de copiar o resto do código para aproveitar o **cache** (se você não mudou as dependências, o Docker não baixa tudo de novo).
        
    - `RUN mvn package`: Compila o código Java e cria um arquivo **.jar** (o aplicativo executável).
        
2. **Estágio Final (`app`):**
    
    - Usa a imagem `diamol/openjdk`. Ela é menor, contendo apenas o necessário para _rodar_ Java, não para compilar.
        
    - `COPY --from=builder ...`: Pega apenas o arquivo **.jar** pronto do estágio anterior.
        
    - `ENTRYPOINT`: Define o comando para iniciar o aplicativo.
        

#### Tente agora: Construindo o App Java

1. Vá para a pasta do exercício: `cd ch04/exercises/image-of-the-day`
    
2. Construa a imagem: `docker image build -t image-of-the-day .`
    

_Seja paciente:_ A primeira vez pode demorar um pouco porque o Docker está baixando as imagens do Maven e todas as dependências do Java dentro do contêiner. Você verá muitos logs do Maven baixando bibliotecas da internet.

#### Rodando a Aplicação Java

Essa aplicação é uma API que consome dados da NASA (Astronomy Picture of the Day). Ela precisa de uma rede para funcionar corretamente.

1. Crie uma rede Docker (para que contêineres possam conversar entre si no futuro): `docker network create nat` _(Se der erro dizendo que já existe, pode ignorar)._
    
2. Rode o contêiner: `docker container run --name iotd -d -p 800:80 --network nat image-of-the-day`
    
3. Teste no navegador: Acesse `http://localhost:800/image`. Você deve ver um JSON com detalhes sobre a foto astronômica do dia (buracos negros, galáxias, etc.).
    

**Conclusão da seção:** Você acabou de compilar e rodar uma aplicação Java complexa sem instalar uma única ferramenta de Java no seu Linux Mint. Tudo foi feito isolado dentro do Docker.

---

**Fim da Seção 4.2.**