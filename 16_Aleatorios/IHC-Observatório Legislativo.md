

---
### **1. Contextualização**
Na era da informação digital, as redes sociais ampliaram drasticamente o alcance e a notoriedade dos debates políticos e da atuação dos deputados federais. No entanto, essa visibilidade nem sempre se traduz em clareza.

Isso gera um novo paradoxo: embora o volume de informação disponível seja o maior da história, encontrar a _verdade_ sobre a atuação parlamentar tornou-se uma tarefa mais difícil. O cidadão vê-se preso entre dois extremos:

1. **Dados Oficiais:** Ricos e precisos, mas apresentados de forma complexa, fragmentada e em jargão técnico nos portais governamentais.
2. **Narrativas de Redes Sociais:** De fácil consumo e alto poder de engajamento, mas frequentemente repletas de desinformação, gráficos enganosos e estatísticas falsas que acabam ofuscando os fatos.    

Este projeto nasce da necessidade de preencher essa lacuna. Nosso objetivo não é apenas "mostrar os dados", mas sim _competir_ com a desinformação, transformando dados públicos em conhecimento acessível, visualmente claro e fácil de compartilhar.
### **2. Objetivo do Projeto**
Desenvolver uma plataforma web que atue como um **antídoto à desinformação**, quebrando a barreira de complexidade dos dados oficiais.

O objetivo é reequilibrar o debate público ao traduzir os dados brutos da Câmara dos Deputados em um formato acessível, intuitivo e visualmente claro. A plataforma permitirá que qualquer cidadão possa fiscalizar, entender e formar opinião sobre a atuação de seus representantes com base em **fatos verificados**.

### **3. Público-Alvo**
Para combater a desinformação de forma eficaz, o projeto foca em dois públicos estratégicos:

- **O Cidadão Fiscalizador:** Pessoas com interesse em política, mas que hoje se sentem frustradas com o volume de narrativas conflitantes e _fake news_. Elas buscam uma fonte  confiável e de fácil digestão para verificar fatos, acompanhar votações-chave e entender os gastos parlamentares, sem a necessidade de conhecimento técnico em análise de dados.
    
- **Os Multiplicadores de Informação:** Jornalistas e criadores de conteúdo digital. Eles necessitam de dados já consolidados, gráficos  e visualizações fáceis de exportar para agilizar seu trabalho de apuração, embasar reportagens, análises e publicações, enriquecendo o debate público com fatos verificados em larga escala.

---
## **5. Funcionalidades**
### 1. Funcionalidades Globais

- **Menu de Navegação no cabeçalho:** Acesso rápido às seções.
- **Barra de Busca Geral:** Permite pesquisar por nome de deputado, partido ou tema.

### 2. Tela Inicial

- **Card "Sessão de Hoje":** Widget que informa se há sessão, qual a pauta principal.
    
- **Transmissão ao Vivo:** Link incorporado para assistir à TV Câmara diretamente no card da sessão com uma imagem. 
    
- **Feed de Notícias:** Destaques curados sobre votações e tramitações relevantes com imagens associadas.

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


Paleta de cores

Light
--text: #061e14;
--background: #f7fcf9;
--primary: #00d66f;
--secondary: #025939;
--accent: #d1fae5;

Dark
--text: #061e14;
--background: #f7fcf9;
--primary: #00d66f;
--secondary: #025939;
--accent: #d1fae5;
