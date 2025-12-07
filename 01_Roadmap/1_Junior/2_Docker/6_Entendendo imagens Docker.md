


---

Uma imagem Docker não é um bloco sólido. Ela é uma coleção lógica de **camadas**.
- A imagem contém os arquivos que você empacotou.
- Ela também contém metadados e um histórico de como foi construída.

Você pode ver exatamente como uma imagem foi criada olhando seu histórico.
```
docker image history web-ping
```

- A coluna **CREATED BY** mostra a instrução do Dockerfile que criou aquela camada.
- Note que as instruções do topo são as mais recentes do seu Dockerfile, e as de baixo vêm da imagem base.
![](../../../attachments/Pasted%20image%2020251207183501.png)

---
### **1. O Conceito de Camadas Compartilhadas**

Isso é fundamental para a eficiência do Docker. As camadas são **somente leitura** e podem ser **compartilhadas** entre diferentes imagens.

Imagine o seguinte cenário:
1. A imagem `diamol/node:2e` base tem o Sistema Operacional e o Node.js.
2. Sua imagem `web-ping` usa essa base e adiciona o arquivo `app.js`.
3. Se você criar outra imagem Node.js, ela também usará a mesma base.

Se você tiver 10 imagens diferentes que usam node:2e como base, o Docker não duplica os arquivos do Node.js 10 vezes. Ele armazena a camada base apenas uma vez e a compartilha com todas as imagens.

![](../../../attachments/Pasted%20image%2020251207183656.png)

---

### 3.5 Otimizando Dockerfiles para usar o cache de camadas

Como as camadas são somente leitura, o Docker pode usar um **cache** durante o processo de _build_ para economizar tempo.

Se você rodar o comando `docker build` novamente sem mudar nada, ele terminará quase instantaneamente. O Docker verifica se a instrução mudou e se os arquivos copiados mudaram. Se nada mudou, ele reutiliza a camada existente (você verá `Using cache` na saída).

#### Quebrando o Cache

Mas, se você mudar algo, o cache daquela etapa em diante é invalidado.

**Tente agora:**

1. Edite o arquivo `app.js` (adicione uma linha vazia no final e salve).
    
2. Construa a imagem novamente como versão 2:
    
    docker image build -t web-ping:v2 .
    

**O que acontece na saída?** 5

- **Step 1 (FROM):** `Using cache` (A base não mudou).
    
- **Step 2 (ENV):** `Using cache` (As variáveis não mudaram).
    
- **Step 3 (WORKDIR):** `Using cache`.
    
- **Step 4 (COPY):** O Docker percebe que o arquivo mudou (pelo hash do arquivo). O cache **não** é usado. Uma nova camada é criada.
    
- **Step 5 (CMD):** Como a etapa anterior mudou, o cache daqui para frente é invalidado automaticamente. Essa etapa é executada novamente.
    

#### A Regra de Ouro da Otimização

Para builds rápidos, você deve ordenar suas instruções no Dockerfile **da menos frequente para a mais frequente**6.

Exemplo de Otimização (Listagem 3.2):

No Dockerfile original, o CMD estava no final. Mas o comando de inicialização raramente muda. O COPY app.js muda sempre que você edita o código.

Um Dockerfile otimizado ficaria assim:

1. `FROM ...` (Muda nunca)
    
2. `CMD ...` (Muda quase nunca)
    
3. `ENV ...` (Muda raramente)
    
4. `WORKDIR ...`
    
5. `COPY app.js .` (Muda frequentemente - **Coloque por último!**)
    

Ao mover o `COPY` para o final, você garante que as etapas anteriores (1, 2, 3 e 4) sejam sempre pegas do cache, tornando o build ultra-rápido mesmo quando você altera o código.

---

### 3.6 Laboratório: Criando uma imagem sem Dockerfile

Chegamos ao desafio prático do capítulo. O objetivo é responder: _"Como criar uma imagem Docker manualmente, sem usar um Dockerfile?"_7.

Isso é útil para entender que uma imagem nada mais é do que o estado congelado de um contêiner.

**O Desafio:**

1. Comece com a imagem `diamol/ch03-lab:2e`.
    
2. Rode um contêiner interativo dela.
    
3. Dentro do contêiner, existe um arquivo `/diamol/ch03.txt`. Edite esse arquivo e adicione seu nome ao final dele.
    
4. Saia do contêiner.
    
5. Crie uma nova imagem a partir desse contêiner modificado.
    

Dicas 8:

- Lembre-se das flags `-it` para rodar interativo.
    
- O sistema de arquivos do contêiner persiste mesmo depois que ele para (Exited).
    
- Explore o comando `docker container --help` para encontrar um comando que "comita" (salva) as mudanças de um contêiner em uma nova imagem. _(Spoiler: procure por `commit`)_.
    

---

**Fim do Capítulo 3.**

Parabéns! Você agora sabe construir, otimizar e gerenciar suas próprias imagens. Podemos avançar para o **Capítulo 4: Empacotando aplicações a partir do código-fonte**?