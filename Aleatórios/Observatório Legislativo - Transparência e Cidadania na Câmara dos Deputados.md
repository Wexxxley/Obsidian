
**1. Contextualização**
Na era da informação digital, as redes sociais ampliaram o alcance e a notoriedade dos debates políticos e da atuação dos deputados federais. No entanto, essa visibilidade nem sempre se traduz em clareza. Há um paradoxo: enquanto o volume de informação aumenta, a capacidade do cidadão comum de compreender e fiscalizar o trabalho de seus representantes diminui, devido à complexidade e à fragmentação dos dados públicos. Este projeto nasce da necessidade de preencher essa lacuna, transformando dados brutos em conhecimento acessível.

**2. O Problema Central**
O acesso às informações públicas sobre a atividade parlamentar, embora garantido por lei, é pouco intuitivo para a maioria dos cidadãos. Os portais oficiais, como o da Câmara dos Deputados, são ricos em dados, mas os apresentam de forma técnica, em planilhas, documentos extensos e com jargão político específico. Isso cria barreiras significativas para o cidadão que deseja:

- Entender como um deputado votou em pautas importantes.
- Acompanhar os projetos de lei propostos.
- Analisar os gastos de verba parlamentar.

**3. Objetivo Geral do Projeto**
Desenvolver uma plataforma web acessível, intuitiva e visualmente clara que traduza dados públicos da Câmara dos Deputados em informações compreensíveis, permitindo que qualquer cidadão possa fiscalizar, entender e interagir com a atuação de seus representantes.

**4. Público-Alvo**
- **Cidadãos Engajados:** Pessoas com interesse em política que desejam acompanhar a atuação dos deputados de forma rápida e confiável, sem a necessidade de conhecimento técnico em análise de dados.
- **Jornalistas e Criadores de Conteúdo:** Profissionais que necessitam de dados consolidados, gráficos e visualizações para embasar reportagens, análises e publicações em redes sociais, agilizando seu trabalho e enriquecendo o debate público.

**5. Proposta de Solução**
Criar uma interface web centrada no usuário, guiada pelos seguintes princípios de Interação Humano-Computador (IHC):

- **Clareza e Simplicidade:** A interface será minimalista, focando no que realmente importa: a informação.
- **Navegação Intuitiva:** Organizar a jornada do usuário de forma lógica, desde a visão geral até os detalhes específicos, com o mínimo de cliques possível.
- **Acessibilidade:** Garantir que a plataforma seja utilizável por pessoas com diferentes níveis de habilidade digital e necessidades especiais (e.g., contraste de cores, compatibilidade com leitores de tela).

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
        
        

### Tema 3: Alinhamento e Comportamento Político

Esta é uma das áreas mais ricas para análise, pois revela o posicionamento real dos deputados.

1. **"Índice de Governismo" (ou Fidelidade Partidária)**
    
    - **O que é:** Um indicador percentual que mostra a frequência com que um deputado vota de acordo com a orientação do Governo ou do seu partido.
        
    - **Tipo de Gráfico:** Gráfico de Medidor (Gauge Chart) ou uma barra de progresso.
        
    - **Por que é interessante:** Responde de forma clara: "Este deputado é da base do governo ou da oposição?". Mede o quão "rebelde" ou alinhado um parlamentar é.
        
2. **"Mapa de Votações Relevantes"**
    
    - **O que é:** Uma matriz visual onde as linhas são deputados e as colunas são votações importantes. As cores indicam o voto (Verde para 'Sim', Vermelho para 'Não', Amarelo para 'Abstenção', Cinza para 'Ausente').
        
    - **Tipo de Gráfico:** Heatmap (Mapa de Calor).
        
    - **Por que é interessante:** Permite identificar padrões e "blocos" de votação de forma muito rápida. Fica fácil ver se um partido votou em uníssono ou se houve dissidentes.
        
3. **"Rede de Alianças em Projetos"**
    
    - **O que é:** Um gráfico que mostra quais deputados costumam assinar projetos de lei em conjunto. Cada deputado é um "nó" e uma linha os conecta se eles forem coautores.
        
    - **Tipo de Gráfico:** Gráfico de Rede/Grafos.
        
    - **Por que é interessante:** Revela alianças e grupos de trabalho que vão além das fronteiras partidárias, mostrando quem realmente trabalha com quem.
        

### Tema 4: Visões Comparativas e Geográficas

Permite que o usuário compare e entenda o contexto regional.

1. **"Mapa Interativo do Brasil"**
    
    - **O que é:** Um mapa do Brasil onde cada estado é colorido de acordo com uma métrica selecionada (ex: Gasto médio por deputado, número de projetos, % de governismo da bancada).
        
    - **Tipo de Gráfico:** Mapa Coroplético.
        
    - **Por que é interessante:** Facilita a comparação entre as bancadas estaduais e a identificação de padrões regionais. É visualmente muito atraente e intuitivo.
        
2. **"Bancadas Temáticas em Foco"**
    
    - **O que é:** Uma análise que agrupa deputados não por partido, mas por frentes parlamentares (as "bancadas", como a ruralista, da segurança, evangélica, etc.) e mostra o comportamento médio delas (gastos, votações, temas de interesse).
        
    - **Tipo de Gráfico:** Gráficos de Barras Comparativas ou Radar Chart para comparar múltiplas métricas.
        
    - **Por que é interessante:** Mostra que a política é organizada por interesses que muitas vezes são mais fortes que as legendas partidárias.
**6. Caráter Extensionista do Projeto**
O caráter extensionista refere-se à capacidade de um projeto de transcender seus próprios muros e dialogar com a sociedade, aplicando o conhecimento gerado para promover transformação social, cultural e cívica. Este projeto é inerentemente extensionista pelos seguintes motivos:
- **Ponte entre a Academia e a Sociedade:** Ele aplica conceitos de Ciência da Computação, Design e Ciência Política (IHC, visualização de dados, análise política) para resolver um problema real da comunidade: a falta de acesso à informação.
- **Empoderamento do Cidadão:** Fornecer informação clara e acessível é uma forma de poder. O projeto empodera o cidadão ao dar-lhe as ferramentas necessárias para cobrar seus representantes com base em dados concretos, e não apenas em discursos.
- **Recurso para a Comunidade:** A ferramenta serve como um bem público digital. Jornalistas, líderes comunitários e outros cidadãos podem utilizar seus recursos gratuitamente para gerar conhecimento, promover debates e fortalecer a democracia local e nacional.
    