
#Concluded 

---
Vamos executar o execício web-ping. O objetivo é verificar se um site está no ar. Ela roda em um contêiner e faz requisições HTTP para uma URL (por padrão, o blog do autor) a cada 3 segundos.

Baixe a imagem da aplicação web-ping:
```
docker image pull diamol/ch03-web-ping:2e
```
A imagem veio do **Docker Hub**, que é o registro padrão onde o Docker procura imagens.

Rode o contêiner em segundo plano (--detach) e dê um nome a ele (--name):
```
docker container run -d --name web-ping diamol/ch03-web-ping:2e
```

Agora, verifique os logs para ver o app funcionando:
```
docker container logs web-ping
```

Esse aplicativo foi programado para ler configurações a partir de variáveis de Ambiente. No Docker, você pode injetar essas variáveis quando inicia o contêiner. Remova o contêiner antigo e inicie um novo, mas desta vez alterando o alvo.
`docker container run --env TARGET=google.com diamol/ch03-web-ping:2e`
- --env define a variável.

![](../../../attachments/Pasted%20image%2020251207155245.png)

