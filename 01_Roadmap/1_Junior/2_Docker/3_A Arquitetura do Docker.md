


---
Existem dois componentes principais que você precisa distinguir:

1. **Docker Engine:** É o processo que roda em segundo plano. Ele gerencia tudo: o cache local de imagens (baixando-as quando necessário), os contêineres ativos, as redes virtuais e os volumes. O Engine expõe todas as suas funcionalidades através de uma API.

2. **Docker CLI:** É a ferramenta de linha de comando que você usa no terminal O CLI é apenas um cliente. Ele não executa os contêineres. Ele apenas envia pedidos para a API do Docker Engine.    

![](../../../attachments/Pasted%20image%2020251207143012.png)

Porque essa sepração é importante?
- **Gerenciamento Remoto:** Como o CLI fala com o Engine via API, você pode usar o CLI no seu laptop para controlar um Docker Engine rodando em um servidor remoto.
- **Interfaces Gráficas:** O CLI não é o único cliente. Interfaces visuais (como o dashboard do Docker Desktop ou ferramentas como Portainer) também se conectam à mesma API para desenhar gráficos de uso de CPU, memória e logs.    


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