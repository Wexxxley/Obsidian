
#Concluded 

---

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

- Cada vez que você roda `docker run`, o Docker cria um **novo contêiner**. É uma nova "caixa" com seu próprio nome e identificação, mesmo que esteja rodando a mesma aplicação.
---
### **1. Fluxo Build, Share and Run**

Este exemplo simples demonstra o fluxo principal do Docker:

1. **Build:** Alguém empacotou a aplicação.
2. **Share:** Alguém publicou a imagem em um site público para que outros pudessem acessar.
3. **Run:** Você, com acesso, rodou a aplicação.

A grande vantagem é que esse fluxo é o mesmo se a aplicação for um script simples ou um sistema bancário complexo em Java. 

---
### **2. Containers interativos** 

Até agora, os contêineres que rodamos executaram uma tarefa rápida e saíram. Mas você pode rodar um contêiner interativo e conectar um terminal a ele, como se estivesse acessando um servidor remoto.

Execute o seguinte comando para rodar um contêiner base e entrar nele:
```
docker run --interactive --tty diamol/base:2e
```

- `--interactive` /`-i`: Mantém a conexão aberta para você interagir.
- `--tty` /`-t`: Simula um terminal de texto.

Você verá que o prompt do seu terminal mudou (algo como / #). Agora você está dentro do contêiner. Tente rodar comandos lá dentro:

1. `hostname`: Vai mostrar o ID do contêiner (ex: `a41ad3...`), provando que ele tem um nome próprio8.
2. `date`: Mostra a data/hora.
3. Para sair, digite `exit`. 

![](../../../attachments/Pasted%20image%2020251207141745.png)

---
### **3. Rodando servidor web**

A maioria das aplicações reais não são scripts interativos, mas sim servidores que rodam continuamente em segundo plano.

Antes de prosseguir, entenda o **ciclo de vida**:

1. Um contêiner roda apenas enquanto o processo principal dele estiver rodando.
2. Quando o processo para, o contêiner entra no estado parado.
3. Um contêiner parado não consome CPU/RAM, mas seus arquivos e logs ainda existem no disco até você removê-lo explicitamente.

Vamos rodar um servidor web simples:
```
docker container run --detach --publish 8088:80 diamol/ch02-hello-diamol-web:2e
```

- `--detach` /`-d`: Roda em segundo plano. O terminal não fica preso; você recebe o ID do contêiner de volta e pode continuar digitando outros comandos.
- `--publish 8088:80` /`-p`: Isso é o mapeamento de portas.

Agora, abra seu navegador e acesse: http://localhost:8088.

![](../../../attachments/Pasted%20image%2020251207142758.png)

---
### **4. Gerenciando containers**

1. **Listar rodando:** `docker container ls` mostra apenas os ativos.
    
2. **Ver processos:** `docker container top <ID>` mostra os processos rodando dentro de um contêiner específico.
    
3. **Ver logs:** `docker container logs <ID>` mostra tudo que o aplicativo escreveu na tela. Isso é crucial para debugar apps que rodam em segundo plano.
    
4. **Inspecionar:** `docker container inspect <ID>` mostra todos os detalhes técnicos (IP, caminhos de disco, variáveis de ambiente) em formato JSON.
