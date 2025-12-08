
---
### **1. Contextualização**
Na era da informação digital, as redes sociais ampliaram drasticamente o alcance e a notoriedade dos debates políticos e da atuação dos deputados federais. No entanto, essa visibilidade nem sempre se traduz em clareza.

Isso gera um novo paradoxo: embora o volume de informação disponível seja o maior da história, encontrar a _verdade_ sobre a atuação parlamentar tornou-se uma tarefa mais difícil. O cidadão vê-se preso entre dois extremos:

1. **Dados Oficiais:** Ricos e precisos, mas apresentados de forma complexa, fragmentada e em jargão técnico nos portais governamentais.
2. **Narrativas de Redes Sociais:** De fácil consumo e alto poder de engajamento, mas frequentemente repletas de desinformação, gráficos enganosos e estatísticas falsas que acabam ofuscando os fatos.    

Este projeto nasce da necessidade de preencher essa lacuna. Nosso objetivo não é apenas "mostrar os dados", mas sim _competir_ com a desinformação, transformando dados públicos brutos em conhecimento acessível, visualmente claro e fácil de compartilhar.
### 2. Objetivo do Projeto
Desenvolver uma plataforma web que atue como um **antídoto à desinformação**, quebrando a barreira de complexidade dos dados oficiais.

O objetivo é reequilibrar o debate público ao traduzir os dados brutos da Câmara dos Deputados em um formato acessível, intuitivo e visualmente claro. A plataforma permitirá que qualquer cidadão possa fiscalizar, entender e formar opinião sobre a atuação de seus representantes com base em **fatos verificados**.

### 3. Público-Alvo
Para combater a desinformação de forma eficaz, o projeto foca em dois públicos estratégicos:

- **O Cidadão Fiscalizador:** Pessoas com interesse em política, mas que hoje se sentem frustradas com o volume de narrativas conflitantes e _fake news_. Elas buscam uma fonte  confiável e de fácil digestão para verificar fatos, acompanhar votações-chave e entender os gastos parlamentares, sem a necessidade de conhecimento técnico em análise de dados.
    
- **Os Multiplicadores de Informação:** Jornalistas e criadores de conteúdo digital. Eles necessitam de dados já consolidados, gráficos  e visualizações fáceis de exportar para agilizar seu trabalho de apuração, embasar reportagens, análises e publicações, enriquecendo o debate público com fatos verificados em larga escala.

### **4. Proposta de Solução**
Criar uma interface web centrada no usuário, guiada pelos seguintes princípios de Interação Humano-Computador (IHC):

**Funcionalidades Principais:**

1. **Perfil do Deputado:** Uma página dedicada para cada parlamentar com:
    - Dados básicos (partido, estado, foto, redes sociais).
    - **Termômetro de Atividade:** Um indicador visual que resume a frequência de presença, discursos e propostas.
    - **Como Votou:** Um registro claro e simplificado das votações mais relevantes, com tags como "A Favor", "Contra", "Abstenção", e um link para o texto do projeto.
    - **Gastos Parlamentares:** Gráficos interativos (pizza, barras) que detalham o uso da cota parlamentar, comparando com a média da casa.
    - **Projetos Apresentados:** Lista de propostas de sua autoria, com status atual.
        
2. **Glossário Político Interativo:** Explicações curtas e acessíveis sobre termos técnicos (ex: "PEC", "Medida Provisória", "Obstrução") que aparecem ao passar o mouse sobre a palavra.
        
3. **Consultas facilitadas:**
	1. **"Raio-X dos Gastos do Deputado"**: Um gráfico de pizza que detalha as categorias de gastos de um parlamentar específico (passagens aéreas, divulgação, etc.).
	    - **Por que é interessante:** Responde à pergunta: "Ok, o deputado gastou R$ 100 mil este mês, mas com o quê?". Permite identificar gastos incomuns 
	        
	2. **"Evolução dos Gastos no Tempo"**: Um gráfico que mostra a variação mensal dos gastos de um deputado, de um partido ou da Câmara como um todo ao longo do ano.
	    - **Por que é interessante:** Permite identificar tendências e picos de gastos. Por exemplo: "Os gastos com divulgação aumentam perto de anos eleitorais?".
	        
	3. **"Principais Focos de Atuação"** Uma nuvem de palavras gerada a partir dos títulos ou ementas dos projetos de lei propostos por um deputado ou partido.
	    - **Por que é interessante:** Oferece uma visão visual e instantânea sobre os temas que mais interessam a um parlamentar (ex: "segurança", "educação", "agronegócio").
        

---

![](../attachments/Pasted%20image%2020251208145502.png)
### **1. Tela Inicial

A home deve ser um painel do que está acontecendo agora.

- **Funcionalidade "Sessão de Hoje":** Um card simples dizendo se há votação no plenário hoje, qual a pauta principal e um link para assistir ao vivo (incorporado da TV Câmara).
- **Noticias recentes.**

### **2. Tela do deputado**


### **3. Tela de Comparação

Uma das maiores dúvidas do eleitor é escolher entre dois candidatos ou comparar seu deputado com o "rival".

- **Funcionalidade:** Permite selecionar dois deputados (ou um Deputado x Média do Estado) e coloca seus dados lado a lado.
    
- **O que compara:**
    - Presença em plenário.
    - Gasto total de cota.
    - Alinhamento com o Governo (Votações iguais à orientação do governo %).
        
- **Recurso para Multiplicadores:** Botão "Gerar Card de Batalha". O sistema cria uma imagem.png pronta com a marca d'água do seu projeto (verificação).

### **4. Match Legislativo**

- **Como funciona:** O usuário não escolhe um deputado. O sistema apresenta 5 votações polêmicas recentes (sem dizer como quem votou). O usuário clica em "A Favor", "Contra" ou "Indiferente".
    
- **Resultado:** O sistema cruza os dados e mostra: _"Você votou 90% igual ao Deputado Fulano"_ ou _"Você pensa o oposto do deputado que você elegeu"_.

### **5. Tela de Bancada: "Raio-X dos Partidos"**

Muitas vezes o deputado é obrigado a seguir o partido. É crucial fiscalizar a agremiação.

- **Coesão Partidária:** Um gráfico mostrando se o partido vota sempre unido ou se é "bagunçado" (cada um vota como quer).
    
- **Top Gastos do Partido:** Ranking de quem são os deputados mais "caros" e mais "econômicos" dentro daquela sigla.
    
- **Nuvem de Ideias:** Quais palavras mais aparecem nos projetos daquele partido? (Ex: Um partido pode falar muito de "Família", outro de "Trabalho", outro de "Liberdade").

### **6. Área do Criador (Hub de Exportação)**

Focada exclusivamente na persona "Multiplicador de Informação".

- **Gerador de Gráficos:** O jornalista configura o gráfico (cor, tipo de dado) e baixa em alta resolução (SVG/PNG) ou embeda o código HTML no site de notícias dele.

### **7. Modo Resumo**

Para projetos de lei (que são textos jurídicos longos e complexos).

- **Funcionalidade:** Uso de IA (Processamento de Linguagem Natural) para resumir a Ementa do Projeto.
    
    - _Texto Original:_ "Altera a Lei nº 9.394... para dispor sobre..."
        
    - _Tradução do Sistema:_ "Este projeto quer obrigar o ensino de robótica em todas as escolas públicas."    



---

## **Definição de Telas e Funcionalidades

### **1. Tela Inicial**

**Objetivo:** Capturar o interesse imediato do usuário pelo "agora" e oferecer portas de entrada rápidas para a fiscalização.

- **Cabeçalho Global:** Logo, Menu de Navegação (Deputados, Partidos, Comparador, Match, Sobre) e Barra de Busca Geral (pesquisa por nome de deputado, partido ou tema).
    
- **Card "Sessão de Hoje":** Widget em destaque informando se há sessão no Plenário, qual a pauta principal do dia e link incorporado para a transmissão ao vivo da TV Câmara.
    
- **Destaques de Notícias:** Feed curado de atualizações relevantes sobre votações e tramitações.

### **2. Tela do Deputado**

**Objetivo:** Centralizar a fiscalização individual, traduzindo dados técnicos em métricas de desempenho e custo compreensíveis.

- **Cabeçalho do Perfil:** Foto oficial, Nome Parlamentar, Partido, Estado (UF), links para redes sociais e botões de ação ("Comparar", "Copiar Link").
    
- **Painel de Desempenho (KPIs):**
    
    - **Presença:** Gráfico de rosca.        
    - **Produção:** Contagem de projetos apresentados vs. aprovados.
        
- **Seção Financeira:**
    - **Evolução de Gastos:** Gráfico de linha (Deputado vs. Média da Câmara).
    - **Top 3 Gastos:** Ícones destacando as categorias mais numerosas (ex: Passagens, Divulgação).
        
- **Seção de Votações:** Lista filtrada das votações de alto impacto (sim/não/abstenção) com link para o "Modo Resumo".
### **3. Tela de Partidos

**Objetivo:** Fiscalizar a instituição partidária, revelando coesão, ideologia real e comportamento de grupo.

- **Cabeçalho da Sigla:** Logo, Nome, Número Eleitoral e tamanho da bancada atual.
    
- **Alinhamento com o Governo:** Taxa percentual de votos favoráveis às pautas do Executivo (define se é Base, Oposição ou Independente).
    
- **Ranking Interno (Gamificação da Bancada):**
    
    - Deputado com maior uso da cota.
        
    - Deputado com menor uso da cota.
        
    - Deputado que mais vota contra a orientação do partido.
        
- **Foco Ideológico:** Nuvem de palavras agregada de todos os membros, revelando as prioridades reais da sigla (ex: Costumes, Economia, Agronegócio).
    
### **4. Tela de Comparação

**Objetivo:** Permitir a análise lado a lado para decisão de voto ou fiscalização comparativa.

- **Seletor de Entidades:** Campos de busca para selecionar "Deputado A" vs. "Deputado B" (ou Deputado vs. Média do Estado).
    
- **Quadro Comparativo:** Tabela visual confrontando:
    
    - Presença em Plenário.
        
    - Gasto total acumulado no ano.
        
    - Alinhamento com o Governo (%).
        
    - Posicionamento em votações chaves.
        
- **Gerador de Card de Batalha:** Botão para exportar a comparação como imagem (PNG) otimizada para redes sociais (Stories/Feed).

### **5. Tela "Match Legislativo"

**Objetivo:** Quebrar viés de confirmação e conectar o cidadão ao representante baseado em ideias, não em nomes.

- **Fluxo do Quiz:** Apresentação sequencial de 5 votações polêmicas recentes (sem revelar autores ou partidos).
    
- **Interação:** O usuário vota "A Favor", "Contra" ou "Indiferente".
    
- **Resultado:** O sistema cruza as respostas do usuário com a base de dados e exibe:
    - "Você pensa 85% igual a esses deputados".

### **6. Área do Criador**

**Objetivo:** Fornecer ferramentas para jornalistas e influenciadores disseminarem dados verificados.

- **Construtor de Gráficos:** Interface para selecionar dados (Gastos, Votações), escolher o tipo de visualização (Pizza, Barras) e personalizar cores.
    
- **Exportação:** Opções de download em alta resolução (SVG, PNG) ou código de incorporação (Embed) para sites de notícias.
    

### **7. Funcionalidades Transversais (Sistema)**

Estas funcionalidades aparecem em várias telas para suporte cognitivo:

- **Modo Resumo (IA):** Botão presente em qualquer menção a Projetos de Lei. Ao clicar, utiliza Processamento de Linguagem Natural para traduzir o "juridiquês" da ementa em uma frase simples de 2 linhas.
    
- **Glossário Político Interativo:** Tooltips (balões de texto) que aparecem automaticamente ao passar o mouse sobre termos técnicos (ex: "Obstrução", "PEC", "Quórum"), explicando-os sem tirar o usuário da página.