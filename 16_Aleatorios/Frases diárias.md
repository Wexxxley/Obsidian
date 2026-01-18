

Para tirar o Observatório Legislativo do papel e transformar o design em um sistema funcional, é preciso de uma combinação de tecnologias de desenvolvimento web.

Para o Front End
- Framework:  React.js
- Estilização: Tailwind CSS
- Gráficos: Bibliotecas como Recharts ou Chart.js permitem criar visualizações responsivas que consomem JSON diretamente.
- Geração de Imagens: Para a funcionalidade de exportar a comparação como imagem PNG, a biblioteca html-to-image seria perfeita, pois ela "tiram um print" de um componente React e o convertem em arquivo para download no navegador do usuário.

Para o Back End
- Backend: FastApi
- Fonte de Dados: A API oficial Dados Abertos da Câmara dos Deputados. é preciso consultar os endpoints e tratar os dados para obter detalhes dos deputados, despesas, votações e proposições. 
- Cache: Como a API da Câmara pode ser lenta ou ter limites de requisição, podemos usar Redis para armazenar dados de acesso frequente.
- Web Scraper: Para dados não disponíveis na API (como certas notícias), pode ser necessário usar técnicas de Web Scrapping
- LLM: Integração via API com OpenAI (GPT-4o-mini) ou Google Gemini para simplificar textos técnicos.


1. Etapa: Análise de Tarefas e Requisitos: Nesta fase, o objetivo é entender o que o sistema deve fazer e como a informação deve ser estruturada.

- **Técnica Utilizada: Classificação de Cartões (Card Sorting)**
    - **Aplicação Prática:** Os participantes receberam cartões físicos com funcionalidades (ex: "Frequência no Plenário", "Ranking") e foram solicitados a agrupá-los e nomeá-los..
        
    - **Levantamento de Requisitos:** Durante essa atividade, foi permitido aos usuários "criar novos cartões com novas funcionalidades", o que configura uma coleta de novos requisitos funcionais não previstos inicialmente.
        
    - **Priorização:** Os usuários também definiram o nível de importância (Indispensável, Importante, Interessante), o que é essencial para a análise de requisitos.

2. Etapa: Prototipação: 
- **Técnica Utilizada: Brainstorming e Prototipação em Papel (Baixa Fidelidade)**
    - **Aplicação Prática:** Foi fornecida uma imagem de uma moldura (base de tela) e pedido para que o participante desenhasse formas geométricas organizando os grupos que ele criou anteriormente.
        
	- **Técnica Utilizada: Entrevista (Perguntas Abertas e Guiadas)** Durante o desenho da tela, foram feitas "Perguntas Guias" como: "Qual desses grupos deve aparecer primeiro?" ou "Se você quiser ver a funcionalidade X, onde você clicaria?".

