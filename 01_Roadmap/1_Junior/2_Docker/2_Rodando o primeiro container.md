
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

### 2. 

Até agora, os contêineres que rodamos executaram uma tarefa rápida e saíram. Mas você pode rodar um contêiner interativo e conectar um terminal a ele, como se estivesse acessando um servidor remoto.

#### Tente agora

Execute o seguinte comando para rodar um contêiner base e entrar nele:

`docker run --interactive --tty diamol/base:2e`

- **`--interactive` (ou `-i`):** Mantém a conexão aberta para você interagir.
    
- **`--tty` (ou `-t`):** Simula um terminal de texto.
    

O que acontece?

Você verá que o prompt do seu terminal mudou (algo como / #). Agora você está dentro do contêiner7.

Tente rodar comandos lá dentro:

1. `hostname`: Vai mostrar o ID do contêiner (ex: `a41ad3...`), provando que ele tem um nome próprio8.
    
2. `date`: Mostra a data/hora.
    

Para sair, digite `exit`. O contêiner irá parar porque o processo do terminal foi encerrado.

#### Gerenciando Contêineres

Agora que você já rodou alguns contêineres, vamos ver como gerenciá-los usando comandos fundamentais.

1. **Listar rodando:** `docker container ls` mostra apenas os ativos.
    
2. **Ver processos:** `docker container top <ID>` mostra os processos rodando dentro de um contêiner específico (como o Gerenciador de Tarefas)9.
    
3. **Ver logs:** `docker container logs <ID>` mostra tudo que o aplicativo escreveu na tela (stdout). Isso é crucial para debugar apps que rodam em segundo plano10.
    
4. **Inspecionar:** `docker container inspect <ID>` mostra todos os detalhes técnicos (IP, caminhos de disco, variáveis de ambiente) em formato JSON11.
    

**Ponto chave:** Para o Docker, todos os contêineres são iguais. Seja um app Java antigo ou um script Python novo, você usa os mesmos comandos (`run`, `ls`, `logs`, `inspect`) para gerenciá-los12.

---

### 2.4 Hospedando um website em um contêiner

A maioria das aplicações reais não são scripts interativos, mas sim servidores (como sites ou APIs) que rodam continuamente em segundo plano.

Antes de prosseguir, entenda o **ciclo de vida**:

- Um contêiner roda apenas enquanto o processo principal dele estiver rodando.
    
- Quando o processo para, o contêiner entra no estado **Exited** (Parado).
    
- Um contêiner parado não consome CPU/RAM, mas seus arquivos e logs ainda existem no disco até você removê-lo explicitamente13.
    

#### Tente agora: Rodando um site "Detached" (em segundo plano)

Vamos rodar um servidor web simples:

`docker container run --detach --publish 8088:80 diamol/ch02-hello-diamol-web:2e`

- **`--detach` (ou `-d`):** Roda em segundo plano. O terminal não fica preso; você recebe o ID do contêiner de volta e pode continuar digitando outros comandos14.
    
- **`--publish 8088:80` (ou `-p`):** Isso é o mapeamento de portas (Port Mapping).
    
    - O tráfego chega no seu computador na porta **8088**.
        
    - O Docker pega esse tráfego e envia para a porta **80** _dentro_ do contêiner15.
        

Agora, abra seu navegador e acesse: http://localhost:8088.

Você verá uma página web simples ("Hello from Chapter 2!"). O site está rodando dentro do contêiner isolado, mas acessível através da porta publicada16.

#### Limpeza

Como aprendemos no Cap. 1, vamos limpar a bagunça:

docker container rm -f $(docker container ls -all -quiet)

Isso para e remove todos os contêineres (rodando ou parados)17.

---

### 2.5 Entendendo como o Docker roda contêineres (Arquitetura)

Por trás dos comandos simples, existe uma arquitetura robusta18:

1. **Docker Client (CLI):** É onde você digita os comandos (`docker run...`). Ele envia requisições para a API do Docker.
    
2. **Docker Engine (Server):** É o processo que fica rodando em segundo plano. Ele recebe os comandos da API e faz o trabalho pesado: baixa imagens, cria contêineres, gerencia redes.
    
3. **Containerd:** O Docker Engine usa um componente chamado _containerd_ para gerenciar o ciclo de vida real dos contêineres. O _containerd_ é um padrão da indústria (usado também pelo Kubernetes), o que significa que o Docker segue padrões abertos (OCI)19.
    

---

### 2.6 Laboratório (Lab)

Chegamos ao desafio prático do capítulo. O objetivo é testar seu conhecimento sem um guia passo-a-passo.

**Desafio:**

1. Rode o contêiner do website (`diamol/ch02-hello-diamol-web:2e`) novamente.
    
2. Substitua o arquivo `index.html` dentro do contêiner por um arquivo seu (com qualquer conteúdo, ex: "Meu Site Hackeado!").
    
3. Acesse o site no navegador e veja sua mudança.
    

Dicas do autor 20:

- Lembre-se que o contêiner tem seu próprio sistema de arquivos.
    
- Nesta imagem específica, o site fica na pasta: `/usr/local/apache2/htdocs/`.
    
- Você precisará de um comando para copiar arquivos do seu computador para dentro do contêiner (lembra do `docker container cp` que mencionei na explicação anterior?).
    

---

**Fim do Capítulo 2.**

Você gostaria da solução do Laboratório ou prefere seguir direto para o **Capítulo 3: Construindo suas próprias imagens Docker**?