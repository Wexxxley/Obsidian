

---
Aplicações reais são sistemas distribuídos: uma API, um site front-end, um banco de dados, um cache Redis, etc. Se você tivesse que rodar tudo isso manualmente, teria que digitar comandos gigantes e gerenciar volumes na mão. 

O **Docker Compose** resolve isso. Ele permite que você escreva um único arquivo descrevendo toda a sua aplicação e a inicie com um único comando.

Para entender o Compose, você precisa entender a mudança de mentalidade:

1. **Imperativo (Scripts):**
    - Você diz o que fazer passo a passo.        
    - Problema: Se você rodar o script duas vezes, ele pode criar contêineres duplicados ou dar erro porque a rede já existe.
        
2. **Declarativo (Docker Compose):**
    
    - Você diz _qual deve ser o resultado final_.
        
    - _"Eu quero um sistema que tenha: 1 serviço web na porta 80 e 1 banco de dados"_.
        
    - Você entrega esse "mapa" para o Docker Compose. Ele olha para o que já está rodando, compara com o mapa e decide o que precisa criar ou atualizar.
        

O Docker Compose é a ferramenta que lê esse mapa (um arquivo YAML) e aplica o estado desejado.

---

### 7.2 O arquivo `docker-compose.yml`

O "mapa" da sua aplicação é escrito em um arquivo chamado `docker-compose.yml`. A sintaxe é simples e legível.

Vamos analisar um exemplo real do livro (Listagem 7.1) para a nossa aplicação **To-Do List**, mas agora separando o site do banco de dados (antes eles rodavam juntos num contêiner só, o que não é ideal).

YAML

```
version: '3.7'  # Versão da sintaxe do Compose

services:       # Aqui listamos os componentes da app
  todo-web:     # Nome do primeiro serviço (Site)
    image: diamol/ch06-todo-list
    ports:
      - "8020:80"    # Mapeia porta 8020 do PC para 80 do container
    networks:
      - app-net      # Conecta na rede 'app-net'

  todo-db:      # Nome do segundo serviço (Banco de Dados)
    image: diamol/postgres:11.5
    ports:
      - "5433:5432"  # Mapeia porta 5433 para 5432 (opcional)
    networks:
      - app-net      # Conecta na MESMA rede

networks:       # Definição das redes
  app-net:      # Cria uma rede chamada 'app-net'
    external:
      name: nat # (Neste exemplo específico, usa uma rede externa)
```

**O que esse arquivo diz?**

> "Docker, eu quero dois serviços: um site (`todo-web`) e um banco (`todo-db`). Quero que ambos estejam na rede `app-net` para poderem conversar entre si. O site deve estar acessível para mim na porta 8020."

#### A Anatomia do Arquivo

1. **`version`**: Define quais recursos do Compose estamos usando (sempre use 3.7 ou superior para compatibilidade moderna).
    
2. **`services`**: É o coração do arquivo. Cada bloco aqui vira um contêiner.
    
    - Você define a `image`, `ports`, `volumes` e `environment` aqui, igual fazia na linha de comando.
        
3. **`networks`** e **`volumes`**: Define a infraestrutura compartilhada.
    

---

### 7.3 Executando aplicações com Docker Compose

Agora vem a mágica. Você não precisa rodar `docker run` para cada serviço.

#### Tente agora:

1. Navegue até a pasta do exercício:
    
    Bash
    
    ```
    cd ~/Documents/Programacao/TestesDocker/diamol/ch07/exercises/todo-list
    ```
    
2. **O Comando Mágico:** Inicie a aplicação inteira.
    
    Bash
    
    ```
    docker-compose up -d
    ```
    
    - `up`: Cria e inicia tudo o que está no arquivo.
        
    - -d (detached): Roda em segundo plano (libera o terminal).
        
        (Nota: Em versões novas do Docker, o comando pode ser docker compose up -d sem o hífen).
        

O que aconteceu?

O Docker Compose leu o arquivo, viu que precisava de dois contêineres, criou a rede necessária e subiu tudo.

3. Verifique o status:
    
    Em vez de docker container ls, usamos:
    
    Bash
    
    ```
    docker-compose ps
    ```
    
    Isso mostra apenas os contêineres **deste projeto** (deste arquivo Compose), ignorando outros contêineres do seu sistema.
    
4. Teste o site:
    
    Acesse http://localhost:8020. Você verá o app To-Do funcionando, mas agora ele está conectado a um banco Postgres real em outro contêiner!
    

---

### 7.4 Gerenciando a aplicação (Parar e Limpar)

O poder do Compose também está em desligar as coisas. Lembra como era chato parar e remover vários contêineres e redes na mão?

1. **Para parar e remover TUDO:**
    
    Bash
    
    ```
    docker-compose down
    ```
    
    - Esse comando para os contêineres.
        
    - Remove os contêineres.
        
    - **Remove a rede** que ele criou para o app.
        
    - (Ele só **não** remove volumes externos, para proteger seus dados).
        

---

### Resumo dos Comandos Essenciais do Compose

|**Comando**|**O que faz?**|
|---|---|
|`docker-compose up -d`|Cria e inicia toda a infraestrutura definida no YAML.|
|`docker-compose down`|Para e remove contêineres, redes e tudo que o `up` criou.|
|`docker-compose ps`|Lista o status dos contêineres deste projeto específico.|
|`docker-compose logs -f`|Mostra os logs de **todos** os serviços misturados (ótimo para debug).|
|`docker-compose stop`|Apenas para os contêineres (não remove).|

Entendeu como o `docker-compose.yml` funciona como uma "receita de bolo" para sua infraestrutura? Podemos ver um exemplo mais complexo ou ir para a próxima parte?