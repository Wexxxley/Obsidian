
#Concluded 

---
### **1. Escrevendo seu primeiro Dockerfile**

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
	
2. **`ENV`**: Define valores para variáveis de ambiente.
    
3. **`WORKDIR`**: Cria um diretório dentro do sistema de arquivos da imagem e define ele como o diretório atual de trabalho.
    
4. **`COPY`**: Copia arquivos ou diretórios do seu computador local para dentro da imagem. Aqui, estamos copiando o código da aplicação (`app.js`) para a pasta de trabalho.
    
5. **`CMD`**: Especifica o comando que será executado quando o Docker iniciar um contêiner a partir desta imagem. 

---
### **2. Construindo imagem a partir do Dockerfile**

O Docker precisa saber a localização dos arquivos que ele vai empacotar. Fique na pasta que deseja empacotar.

Execute o seguinte comando para transformar seu Dockerfile em uma imagem:
`docker image build --tag web-ping .`

- `--tag`/`-t`: Define o nome da imagem como web-ping.
- `.`: Ele diz ao Docker que o build context é o diretório atual. O Docker vai pegar todos os arquivos desta pasta e enviar para o motor construir a imagem.

Agora que a imagem foi construída, ela está armazenada no seu computador. Agora você pode executala: 
![](../../attachments/Pasted%20image%2020251207183011.png)
