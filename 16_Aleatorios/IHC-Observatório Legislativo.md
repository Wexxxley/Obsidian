
---
### **1. Contextualização**
Na era da informação digital, as redes sociais ampliaram drasticamente o alcance e a notoriedade dos debates políticos e da atuação dos deputados federais. No entanto, essa visibilidade nem sempre se traduz em clareza.

Isso gera um novo paradoxo: embora o volume de informação disponível seja o maior da história, encontrar a _verdade_ sobre a atuação parlamentar tornou-se uma tarefa mais difícil. O cidadão vê-se preso entre dois extremos:

1. **Dados Oficiais:** Ricos e precisos, mas apresentados de forma complexa, fragmentada e em jargão técnico nos portais governamentais.
2. **Narrativas de Redes Sociais:** De fácil consumo e alto poder de engajamento, mas frequentemente repletas de desinformação, gráficos enganosos e estatísticas falsas que acabam ofuscando os fatos.    

Este projeto nasce da necessidade de preencher essa lacuna. Nosso objetivo não é apenas "mostrar os dados", mas sim _competir_ com a desinformação, transformando dados públicos brutos em conhecimento acessível, visualmente claro e fácil de compartilhar.
### **2. Objetivo do Projeto**
Desenvolver uma plataforma web que atue como um **antídoto à desinformação**, quebrando a barreira de complexidade dos dados oficiais.

O objetivo é reequilibrar o debate público ao traduzir os dados brutos da Câmara dos Deputados em um formato acessível, intuitivo e visualmente claro. A plataforma permitirá que qualquer cidadão possa fiscalizar, entender e formar opinião sobre a atuação de seus representantes com base em **fatos verificados**.

### **3. Público-Alvo**
Para combater a desinformação de forma eficaz, o projeto foca em dois públicos estratégicos:

- **O Cidadão Fiscalizador:** Pessoas com interesse em política, mas que hoje se sentem frustradas com o volume de narrativas conflitantes e _fake news_. Elas buscam uma fonte  confiável e de fácil digestão para verificar fatos, acompanhar votações-chave e entender os gastos parlamentares, sem a necessidade de conhecimento técnico em análise de dados.
    
- **Os Multiplicadores de Informação:** Jornalistas e criadores de conteúdo digital. Eles necessitam de dados já consolidados, gráficos  e visualizações fáceis de exportar para agilizar seu trabalho de apuração, embasar reportagens, análises e publicações, enriquecendo o debate público com fatos verificados em larga escala.


---
## **4. Possíveis telas**

### **1. Tela Inicial**

- **Cabeçalho Global:** Logo, Menu de Navegação (Deputados, Partidos, Comparador, Match, Sobre) e Barra de Busca Geral (pesquisa por nome de deputado, partido ou tema).
    
- **Card "Sessão de Hoje":** Widget em destaque informando se há sessão no Plenário, qual a pauta principal do dia e link incorporado para a transmissão ao vivo da TV Câmara.
    
- **Destaques de Notícias:** Feed curado de atualizações relevantes sobre votações e tramitações.
![](../attachments/Pasted%20image%2020251209075113.png)
### **2. Tela do Deputado**

- **Cabeçalho do Perfil:** Foto oficial, Nome Parlamentar, Partido, Estado (UF), links para redes sociais e botões de ação ("Comparar", "Copiar Link").
    
- **Painel de Desempenho (KPIs):**
    - **Presença:** Gráfico de rosca.        
    - **Produção:** Contagem de projetos apresentados vs. aprovados.
        
- **Seção Financeira:**
	- Gráfico mostranod os gastos parlamentares por tipo (viagem, divulgação, abastecimento e etc.) e a comparação com a media de gastos dos parlmantares. Gráfico de barras lado a lado horizontalmente
        
- **Seção de Votações:** Lista filtrada das votações de alto impacto (sim/não/abstenção) com link para o "Modo Resumo".

- Ultimas noticias relacionadas a esse deputado

![](../attachments/Pasted%20image%2020251209075618.png)
### **3. Tela de Partidos**

- **Cabeçalho da Sigla:** Logo, Nome, Número Eleitoral e tamanho da bancada atual.
    
- **Ranking Interno (Gamificação da Bancada):**
    - Deputado com maior uso da cota.
    - Deputado com menor uso da cota.
    - Deputado que mais vota contra a orientação do partido.
    
- Ultimas noticias relacionadas a esse partido

- Deputados asociados.

![](../attachments/Pasted%20image%2020251209080053.png)
### **4. Tela de Comparação**

**Objetivo:** Permitir a análise lado a lado para decisão de voto ou fiscalização comparativa.

- **Seletor de Entidades:** Campos de busca para selecionar "Deputado A" vs. "Deputado B" (ou Deputado vs. Média do Estado).
    
- **Quadro Comparativo:** Tabela visual confrontando:
    - Presença em Plenário
    - Gasto total acumulado no ano.
    - Alinhamento com o Governo (%).
    - Posicionamento em votações chaves.
    
- Gastos por gategoria, comparação

- Posicionamento em algumas votaçoes importantes
        
- **Gerador de Card de Batalha:** Botão para exportar a comparação como imagem (PNG) otimizada para redes sociais (Stories/Feed).
![](../attachments/Pasted%20image%2020251209080515.png)
### **5. Tela "Match Legislativo"**

**Objetivo:** Quebrar viés de confirmação e conectar o cidadão ao representante baseado em ideias, não em nomes.

- **Fluxo do Quiz:** Apresentação sequencial de 5 votações polêmicas recentes (sem revelar autores ou partidos).
    
- **Interação:** O usuário vota "A Favor", "Contra" ou "Indiferente".
    
- **Resultado:** O sistema cruza as respostas do usuário com a base de dados e exibe:

![](../attachments/Pasted%20image%2020251209080835.png)

### **6. Tela de Detalhes da Proposição**

- **Cabeçalho do Projeto:** Título oficial em destaque (ex: PL 2630/2020), Autor principal (com link para o perfil) e Data de apresentação.     
    
- **"O Que Muda na Minha Vida?" (IA):** Este é o coração da tela. Um box em destaque que utiliza o **Modo Resumo** para explicar o impacto prático da lei, substituindo a ementa técnica.     - _Exemplo:_ Em vez de "Altera a lei 12.3...", exibe: _"Este projeto proíbe o uso de celulares em salas de aula de escolas públicas e privadas."_     
    
- **Timeline Visual (Rastreador de Tramitação):** Uma barra de progresso horizontal (estilo status de pedido de app de entrega) mostrando visualmente onde o projeto está travado ou andando:     - _Etapas:_ Apresentação ➔ Comissões ➔ Plenário ➔ Senado ➔ Sanção Presidencial.     
    
- **Enquete Cidadã:** Um widget de engajamento perguntando: _"Você apoiaria esse projeto?"_ (Sim / Não). Exibe a porcentagem da opinião dos usuários da plataforma em tempo real.     
    
- **Documentos Originais:** Para o perfil "Multiplicador/Jornalista", um link discreto para baixar o PDF original do projeto e ver o histórico técnico completo.

- Se ja votado, uma lista exportavel com os votos de cada deputado.

![](../attachments/Pasted%20image%2020251209081236.png)

---

## **5. Funcionalidades**
### 1. Funcionalidades Globais

- **Menu de Navegação:** Acesso rápido às seções Deputados, Partidos, Comparador, Match e Sobre.
- **Barra de Busca Geral:** Permite pesquisar por nome de deputado, partido ou tema.

### 2. Tela Inicial

- **Card "Sessão de Hoje":** Widget que informa se há sessão, qual a pauta principal.
    
- **Transmissão ao Vivo:** Link incorporado para assistir à TV Câmara diretamente no card da sessão.
    
- **Feed de Notícias:** Destaques curados sobre votações e tramitações relevantes.

### 3. Tela do Deputado

- **Perfil do Parlamentar:** Exibição de foto, nome, partido, estado, links para redes sociais e botões de ação ("Comparar", "Copiar Link").
    
- **Painel de Presença:** Gráfico de rosca mostrando a assiduidade do deputado.
    
- **Indicador de Produção:** Contagem comparativa de projetos apresentados versus aprovados.
    
- **Análise Financeira:**
    - Gráfico de gastos por tipo (viagem, divulgação, etc.).
    - Comparação dos gastos do deputado com a média dos parlamentares.
    
- **Histórico de Votações:** Lista filtrada de votações de alto impacto (Sim/Não/Abstenção).
    
- **Notícias Relacionadas:** Feed de últimas notícias específicas sobre o deputado.

### 4. Tela de Partidos

- **Cabeçalho:** Exibição de logo, nome, número eleitoral e tamanho da bancada.
    
- **Ranking Interno:** Exibição de destaques da bancada, incluindo:
    - Deputado com maior uso da cota parlamentar.
    - Deputado com menor uso da cota.
    - Deputado mais "rebelde" (que mais vota contra a orientação do partido).
    
- **Feed do Partido:** Últimas notícias relacionadas à sigla.
    
- **Lista de Membros:** Relação dos deputados associados ao partido.

### 5. Tela de Comparação

- **Seletor de Entidades:** Busca para selecionar "Deputado A" vs. "Deputado B" (ou vs. Média do Estado) para confronto direto.
    
- **Quadro Comparativo Visual:** Tabela lado a lado exibindo:
    - Presença em Plenário.
    - Gasto total acumulado e gastos por categoria.
    - Porcentagem de alinhamento com o Governo.
    - Posicionamento em votações-chave.
        
- **Gerador de "Card de Batalha":** Botão para exportar a comparação como uma imagem (PNG) otimizada para redes sociais.

### 6. Tela "Match Legislativo"

- **Quiz Interativo:** Apresentação sequencial de 5 votações polêmicas recentes, sem revelar autores ou partidos.
- **Sistema de Votação do Usuário:** Interface para o usuário votar "A Favor", "Contra" ou "Indiferente".
- **Resultado do Match:** Cruzamento das respostas do usuário com a base de dados para exibir os deputados com maior afinidade ideológica.

### 7. Tela de Detalhes da Proposição

- **Cabeçalho do Projeto:** Título oficial (ex: PL 2630/2020), autor principal e data.
    
- Funcionalidade "O Que Muda na Minha Vida?" (IA): Box que utiliza IA para traduzir a ementa técnica em uma explicação do impacto prático da lei.
    
- **Timeline Visual:** Barra de progresso mostrando a etapa atual da tramitação (Comissões, Plenário, Senado, Sanção).
    
- **Enquete Cidadã:** Widget de engajamento perguntando se o usuário apoiaria o projeto.
    
- **Resultado da Enquete:** Exibição em tempo real da porcentagem de opinião dos usuários da plataforma.
    
- **Download de Documentos:** Link para baixar o PDF original do projeto.
    
- **Lista de Votos Exportável:** Se o projeto já foi votado, exibe e permite exportar a lista de votos de cada deputado.

---

O Observatório Legislativo lida com dados complexos. O maior desafio é a Arquitetura da Informação. 

**Parte 1: Card Sorting**
1. Vamos dar cartões físicos misturados ao participante. 
    
2. Pedir para ele agrupar.
    
3. Nesse momento ele pode criar novos cartões com novas funcionalidades
    
4. Quando ele terminar e nomear os grupos, vamos utilizar esses nomes no menu do prototipo.

**Parte 2: Co-Design

Essa imagem sera a base utilizada pelo participante.
![450](../attachments/Pasted%20image%2020251211094525.png)

- "Agora que organizamos os grupos, vamos desenhar como isso aparece na tela. Imagine esta moldura como a tela inicial do site."
    
- Vamos pedir ao participante para desenhar (formas geométricas) nas telas e ordenar como ele deciciu anteriormente. A ideia é ir modelando de tela em tela.
    
- **Perguntas Guias:**
    - "Qual desses grupos deve aparecer primeiro ou ser maior na tela?"
    - "Se você quiser ver a funcionalide X, onde você clicaria?"

---
### **Lista de Cartões**

- **Status da Sessão ao Vivo** (Se há sessão no Plenário agora e qual a pauta)
    
- **Transmissão TV Câmara** (Vídeo ao vivo da sessão)
    
- **Feed de Notícias** (Atualizações sobre votações e tramitações)
    
- **Perfil do Deputado** (Foto, Nome, Partido e Estado)
    
- **Gráfico de Presença** (Assiduidade do parlamentar no ano)
    
- **Projetos Apresentados vs. Aprovados de um dep**  (Quantidade de leis criadas)
    
- **Gráfico de Gastos de um dep por Categoria** (Quanto gastou com viagens, divulgação, etc.)
    
- **Comparação de Gastos com a Média** (Se o deputado gasta mais ou menos que os outros)
    
- **Histórico de Votações** (Como o deputado votou em projetos importantes: Sim/Não)
    
- **Explicação Simplificada (IA) de uma lei** (Resumo fácil de entender sobre o que muda na lei)
    
- **Resumo do Partido** (Tamanho da bancada e informações da sigla)
    
- **Lista de Membros do Partido** (Todos os deputados daquela sigla)
    
- **Ranking: O "Mais Gastão"** (Deputado que mais usou a cota no partido)
    
- **Ranking: O "Mais Econômico"** (Deputado que menos usou a cota no partido)
    
- **Ranking: O "Mais Rebelde"** (Deputado que vota contra o próprio partido)
    
- **Barra de Tramitação** (Visualização de onde o projeto está parado: Câmara, Senado ou Presidente)
    
- **Download do Projeto Original** (Link para o documento PDF oficial)
    
- **Lista de Votos do Projeto** (Quem votou Sim e quem votou Não em uma lei específica)

- **Barra de Busca** (Pesquisar por nome, partido ou tema)
    
- **Comparar Deputados** (Selecionar dois políticos para ver lado a lado)
    
- **Quiz "Match Legislativo"** (Responder perguntas para descobrir afinidade com políticos)
    
- **Votar em Enquete** (Dizer se você apoia ou não um projeto de lei)
