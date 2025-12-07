


---

Vamos executar o execício web-ping. O objetivo dela é verificar se um site está no ar. Ela roda em um contêiner e faz requisições HTTP para uma URL (por padrão, o blog do autor) a cada 3 segundos.

Baixe a imagem da aplicação web-ping:
```
docker image pull diamol/ch03-web-ping:2e
```

A imagem veio do **Docker Hub**, que é o registro padrão onde o Docker procura imagens.

Rode o contêiner em segundo plano (--detach ou -d) e dê um nome a ele (--name):
```
docker container run -d --name web-ping diamol/ch03-web-ping:2e
```

Agora, verifique os logs para ver o app funcionando:
```
docker container logs web-ping
```

Você verá que o app está pingando o blog do autor (`blog.sixeyed.com`) a cada 3000ms.

---
### **1. Variáveis de ambiente**

Esse aplicativo foi programado para ler configurações a partir de variáveis de Ambiente do sistema. No Docker, você pode injetar essas variáveis quando inicia o contêiner. Remova o contêiner antigo e inicie um novo, mas desta vez alterando o alvo.
`docker container run --env TARGET=google.com diamol/ch03-web-ping:2e`

- --env ou -e define a variável.

A imagem Docker vem com configurações padrão, mas o autor da imagem deve permitir flexibilidade. O código da aplicação web-ping procura uma variável chamada TARGET. Se você fornecer um valor diferente na hora de rodar (docker run), o comportamento do app muda sem você precisar alterar o código ou reconstruir a imagem.

![](../../../attachments/Pasted%20image%2020251207155245.png)

---
### **2. Escrevendo seu primeiro Dockerfile**

O Dockerfile é um script simples contendo instruções para empacotar uma aplicação. A saída desse script é uma Imagem Docker.

Abaixo está o Dockerfile completo para a aplicação `web-ping`:

```Dockerfile
FROM diamol/node:2e
ENV TARGET="blog.sixeyed.com"
ENV METHOD="HEAD"
ENV INTERVAL="3000"
WORKDIR /web-ping
COPY app.js .
CMD ["node", "/web-ping/app.js"]
```

1. **`FROM`**: Especifica a imagem base. Ao criar uma aplicação qualquer, você precisa de uma imagem base para fornecer o "chão" onde sua aplicação vai pisar.
	- Vai fazer um site em Node? `FROM node:18`
	- Vai fazer um script em Python? `FROM python:3.9`
	- Vai fazer um programa em Java? `FROM openjdk:17`
	
2. **`ENV`**: Define valores para variáveis de ambiente (Environment Variables). Aqui 
    
3. **`WORKDIR`**: Cria um diretório dentro do sistema de arquivos da imagem e define ele como o diretório atual de trabalho.
    
4. **`COPY`**: Copia arquivos ou diretórios do seu computador local (o host) para dentro da imagem. Aqui, estamos copiando o código da aplicação (`app.js`) para a pasta de trabalho.
    
5. **`CMD`**: Especifica o comando que será executado quando o Docker iniciar um contêiner a partir desta imagem. Aqui, ele manda o Node executar o arquivo javascript.

Essas 5 instruções são praticamente tudo o que você precisa para empacotar suas próprias aplicações.

Para construir essa imagem, você precisa dos arquivos no seu computador Navegue até a pasta do exercício. Você verá dois arquivos: `Dockerfile` e `app.js`. O `app.js` é o código da aplicação Node.js

![](../../../attachments/Pasted%20image%2020251207154916.png)
