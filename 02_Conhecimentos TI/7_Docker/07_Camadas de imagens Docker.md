
#Concluded 

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
![](../../attachments/Pasted%20image%2020251207183501.png)

---
### **1. Camadas Compartilhadas**

Isso é fundamental para a eficiência do Docker. As camadas são **somente leitura** e podem ser **compartilhadas** entre diferentes imagens.

Imagine o seguinte cenário:
1. A imagem `diamol/node:2e` base tem o Sistema Operacional e o Node.js.
2. Sua imagem `web-ping` usa essa base e adiciona o arquivo `app.js`.
3. Se você criar outra imagem Node.js, ela também usará a mesma base.

Se você tiver 10 imagens diferentes que usam node:2e como base, o Docker não duplica os arquivos do Node.js 10 vezes. Ele armazena a camada base apenas uma vez e a compartilha com todas as imagens.

![](../../attachments/Pasted%20image%2020251207183656.png)

---
### **2. Otimizando Dockerfiles para usar o cache de camadas**

Como as camadas são somente leitura, o Docker pode usar um cache durante o processo de _build_ para economizar tempo.

Se você rodar o comando `docker build` novamente sem mudar nada, ele terminará quase instantaneamente. O Docker verifica se a instrução mudou e se os arquivos copiados mudaram. Se nada mudou, ele reutiliza a camada existente.

Para builds rápidos, você deve ordenar suas instruções no Dockerfile **da menos frequente para a mais frequente**.

No Dockerfile original, o CMD estava no final. Mas o comando de inicialização raramente muda. O COPY app.js muda sempre que você edita o código.

Um Dockerfile otimizado ficaria assim:

1. `FROM ...` (Muda nunca)
2. `CMD ...` (Muda quase nunca)
3. `ENV ...` (Muda raramente)
4. `WORKDIR ...`
5. `COPY app.js .` (Muda frequentemente - **Coloque por último!**)

Ao mover o COPY para o final, você garante que as etapas anteriores sejam sempre pegas do cache, tornando o build mais rápido mesmo quando você altera o código.
![](../../attachments/Pasted%20image%2020251208065556.png)