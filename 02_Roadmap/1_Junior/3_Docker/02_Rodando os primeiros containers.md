
#Concluded 

---
### **1. Hello world** 

Digite o seguinte comando para rodar o contêiner Hello World:
```bash
docker run hello-world
```

O objetivo desse contêiner é ser o mais leve possível e confirmar que o docker está funcionando na sua máquina.

1. O Docker checa se você já tem a imagem `hello-world` salva localmente.
2. Se não tiver, ele busca e baixa a imagem (faz o pull) do repositório Docker Hub.
3. O Docker cria e inicia um novo contêiner a partir dessa imagem.
4. O código dentro do contêiner é executado. Esse código simplesmente imprime uma mensagem no seu terminal, e então o contêiner encerra a execução.

![](../../../attachments/Pasted%20image%2020251207140344.png)

- Cada vez que você roda `docker run`, o Docker cria um **novo contêiner**. É uma nova "caixa" com seu próprio nome e identificação, mesmo rodando a mesma aplicação.

---
### **2. Rodando servidor web**

A maioria das aplicações reais são servidores que rodam continuamente em segundo plano. Antes de prosseguir, entenda o **ciclo de vida**:

1. Um contêiner roda apenas enquanto o processo principal dele estiver rodando.
2. Quando o processo para, o contêiner entra no estado parado.
3. Um contêiner parado não consome CPU/RAM, mas seus arquivos e logs ainda existem no disco até você removê-lo explicitamente.

Vamos rodar um servidor web simples:
```
docker container run --detach --publish 8088:80 diamol/ch02-hello-diamol-web:2e
```

- `--detach` /`-d`: Roda em segundo plano. O terminal não fica preso.
- `--publish 8088:80` /`-p`: Isso é o mapeamento de portas.

Agora, abra seu navegador e acesse: http://localhost:8088.

![](../../../attachments/Pasted%20image%2020251207142758.png)
