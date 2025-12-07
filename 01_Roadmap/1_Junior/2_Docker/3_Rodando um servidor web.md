


---

Por trás dos comandos simples, existe uma arquitetura robusta:

1. **Docker Client (CLI):** É onde você digita os comandos. Ele envia requisições para a API do Docker.
2. **Docker Engine (Server):** É o processo que fica rodando em segundo plano. Ele recebe os comandos e faz o trabalho pesado: baixa imagens, cria contêineres, gerencia redes.
3. **Containerd:** O Docker Engine usa um componente chamado _containerd_ para gerenciar o ciclo de vida real dos contêineres. O _containerd_ é um padrão da indústria (usado também pelo Kubernetes), o que significa que o Docker segue padrões abertos (OCI)19.

![](../../../attachments/Pasted%20image%2020251207143012.png)
Peço desculpas por ter resumido demais. Você tem toda razão: entender a arquitetura (2.5) e o desafio prático (2.6) em profundidade é fundamental para não ficar apenas "decorando comandos".

Aqui está a tradução e explicação detalhada e expandida dessas duas seções finais do Capítulo 2.

#### A Arquitetura do Docker: Peças Móveis

Instalar o Docker parece simples, mas você na verdade instalou uma plataforma com vários componentes. 

Existem dois componentes principais que você precisa distinguir:

1. Docker Engine: É o processo que roda em segundo plano. Ele gerencia tudo: o cache local de imagens (baixando-as quando necessário), os contêineres ativos, as redes virtuais e os volumes.O Engine expõe todas as suas funcionalidades através de uma **API** (Docker API).
    
- **Importante:** A Docker API é uma API REST padrão baseada em HTTP. Isso significa que qualquer software pode "conversar" com o Docker Engine se tiver permissão.
    

2. Docker CLI (O "Cliente")

- É a ferramenta de linha de comando que você usa no terminal (`docker container run...`).
    
- O CLI é apenas um **cliente**. Ele não executa os contêineres. Ele apenas envia pedidos (requests) para a API do Docker Engine.
    
- O Engine recebe o pedido, faz o trabalho pesado e devolve a resposta para o CLI exibir na sua tela.
    

#### Por que essa separação importa?

Entender que o CLI e o Engine são separados abre possibilidades poderosas:

- **Gerenciamento Remoto:** Como o CLI fala com o Engine via API, você pode usar o CLI no seu laptop para controlar um Docker Engine rodando em um servidor na nuvem, ou num Raspberry Pi na sua mesa. O comando é o mesmo, você só aponta o CLI para outro lugar.
    
- **Interfaces Gráficas (GUIs):** O CLI não é o único cliente. Interfaces visuais (como o dashboard do Docker Desktop ou ferramentas como Portainer) também se conectam à mesma API para desenhar gráficos de uso de CPU, memória e logs.
    

#### O que há dentro do Engine? (Containerd e OCI)

O autor explica que não precisamos mergulhar muito fundo, mas é bom saber o seguinte:

- O Docker Engine usa um componente chamado **containerd** para gerenciar a vida dos contêineres de fato.
    
- O **containerd** é um projeto _Open Source_ supervisionado pela CNCF (Cloud Native Computing Foundation).
    
- Existe um padrão aberto para como contêineres devem rodar, chamado **OCI (Open Container Initiative)** .
    

**O que isso significa para você?** Significa que você não está preso ao vendedor "Docker Inc.". Como a tecnologia segue padrões abertos (OCI), você pode trocar o Docker por outras ferramentas (como Podman ou Rancher) no futuro sem precisar reconstruir todas as suas aplicações. O conhecimento é transferível.

---

### 2.6 Laboratório: Modificando um contêiner vivo (Aprofundado)

Os laboratórios deste livro são projetados para fazer você pensar, não apenas copiar. Neste primeiro desafio, o objetivo é responder à pergunta: _"Como altero algo dentro de um contêiner que já está rodando?"_.

Embora o ideal seja automatizar tudo via _Dockerfile_, às vezes você precisa entrar em um contêiner para testar uma mudança rápida ou investigar um erro manualmente.

A Tarefa

1. Execute o contêiner do website que usamos antes (`diamol/ch02-hello-diamol-web:2e`).
    
2. Sua missão é **substituir o arquivo `index.html`** original por um arquivo novo, criado por você, com o conteúdo que você quiser.
    
3. Ao atualizar a página no navegador, você deve ver o seu novo conteúdo, provando que alterou o sistema de arquivos do contêiner.
    

As Pistas (Hints)

O autor fornece dicas cruciais para resolver isso sem te dar a resposta pronta:

1. **Descubra os comandos:** Se você digitar `docker container --help`, verá uma lista de tudo o que pode fazer com um contêiner. Procure por algo que soe como "copiar arquivos" (copy).
    
2. **Onde está o site?** O autor informa que, nesta imagem específica, o servidor web (Apache) busca os arquivos na pasta:
    
    - `/usr/local/apache2/htdocs/`
        
    - _(Nota: Caminhos em contêineres Linux sempre usam barras normais `/`, mesmo se você estiver no Windows)._
        
3. **Persistência:** Lembre-se do que aprendemos antes: o sistema de arquivos do contêiner existe enquanto o contêiner existir. Se você copiar um arquivo para lá, ele fica lá até você apagar o contêiner.
    

#### Raciocínio para a Solução (Passo a Passo Mental)

Para resolver isso, você precisaria:

1. Criar um arquivo `index.html` no seu computador (pode ser no Bloco de Notas) escrevendo algo como `<h1>Fui Hackeado pelo Aluno!</h1>`.
    
2. Rodar o contêiner do site em modo _detached_ (segundo plano) e com a porta mapeada, para que você possa acessá-lo.
    
3. Usar o comando de cópia do Docker (`cp`) para pegar o arquivo do **seu PC** e jogá-lo para **dentro do contêiner**, especificamente na pasta que o autor revelou (`/usr/local/apache2/htdocs/`).
    
4. Dar um _refresh_ no navegador.
    

Esta tarefa ensina você a transpor a barreira entre "meu computador" e "o computador do contêiner".

---

**Isso cobre com profundidade total o final do Capítulo 2.**

Agora que fechamos a base de execução e arquitetura, o próximo passo lógico é parar de usar as imagens do autor e começar a criar as suas.

Podemos iniciar o **Capítulo 3: Construindo suas próprias imagens Docker**?