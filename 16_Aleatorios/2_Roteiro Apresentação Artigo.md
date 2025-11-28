

---
#### **1. Apresentação dos integrantes e do tema:** 

Este artigo apresenta uma prova de conceito (POC) de uma arquitetura de software integrada, distribuída como um aplicativo, projetada para simplificar a coleta, tratamento, armazenamento e a análise de dados abertos da Câmara dos Deputados. 

O objetivo deste protótipo é validar uma arquitetura de fácil distribuição que sirva como um ponto de partida para a análise de dados parlamentares. A solução consiste em um sistema automatizado que extrai e estrutura dados de deputados, despesas, partidos e sessões e votações em um banco de dados local. 

Uma API local serve esses dados para uma amostra de interface de visualização em HTML, que apresenta gráficos sobre as principais consultas de interesse público, como gastos por parlamentar e alinhamento de votos.

### 2. Problematização

O principal desafio enfrentado neste projeto foi a extrema heterogeneidade dos dados fornecidos pela Câmara.

- **Lógicas de Extração Distintas:** A obtenção de um conjunto completo de dados raramente é uma única chamada de API. Frequentemente, é preciso primeiro fazer uma requisição-mãe (ex: votações, em JSON) e, em seguida, acessar links internos dessa resposta (ex: os votos individuais, em XML) para obter detalhes e até mesmo acessar outros endpoints para completar as informações relevantes de uma entidade.

- **Formatos Múltiplos:** Os dados não estão em formato único. Dependendo do endpoint, as informações vêm em JSON, XML ou CSV.

### 3. 





#### **Slide 1**
**(Tempo estimado: 1 min)**

- **Fala Sugerida:** "Olá a todos. Me chamo [Seu Nome] e, juntamente com meus colegas, desenvolvemos o trabalho intitulado **'Ferramenta Integrada para Extração e Visualização de Dados Parlamentares Abertos'**1111.
    
- **Contexto:** Este projeto foi desenvolvido no contexto da Universidade Federal do Ceará 2 e visa apresentar uma Prova de Conceito (POC) de software para facilitar o controle social sobre a Câmara dos Deputados."
    

#### **Slide 2: A Problematização (O Cenário Atual)**

**(Tempo estimado: 2 min)**

- **Tópico Principal:** A transparência vs. Acessibilidade Técnica.
    
- **Fala Sugerida:** "Vivemos hoje numa era de 'dilúvio de dados'3. Embora a transparência governamental seja essencial e existam portais como o da Câmara dos Deputados que oferecem um volume massivo de informações4444, existe uma barreira invisível.
    
    - A mera existência do dado não garante transparência5.
        
    - Para o cidadão comum, e até para jornalistas, os dados estão fragmentados em formatos heterogêneos como JSON, XML e CSV6666.
        
    - **O Problema Central:** Sem conhecimento em programação para consumir APIs complexas, o cidadão não consegue transformar esses dados brutos em informação útil para fiscalização7777. É aqui que nosso trabalho atua."
        

#### **Slide 3: A Solução Proposta (O Analisador Parlamentar)**

**(Tempo estimado: 1 min)**

- **Tópico Principal:** Simplificação e Automação.
    
- **Fala Sugerida:** "Para resolver isso, propomos uma arquitetura de software distribuída como um aplicativo desktop único888.
    
- O objetivo não é apenas baixar dados, mas encapsular todo o ciclo de vida da informação: Coleta, Tratamento, Armazenamento e Visualização9.
    
- Nós criamos uma ferramenta que automatiza o processo de ETL (_Extract, Transform, Load_), entregando ao usuário final gráficos prontos e, ao pesquisador, um banco de dados limpo e estruturado10101010."
    

#### **Slide 4: Demonstração Prática (Ao Vivo)**

**(Tempo estimado: 2 min - Foco na execução)**

- **Ação:** _[Trocar a tela para a aplicação. Abrir o executável.]_
    
- **Fala durante a preparação:** "Vou demonstrar a execução da ferramenta agora. Como se trata de uma Prova de Conceito, focamos na facilidade de distribuição. O usuário seleciona o ano desejado — vamos usar 2011 como exemplo — e inicia o processamento11."
    
- **Ação:** _[Clicar em "Iniciar Processamento" e deixar o log rolando na tela - ver Fig 3 do PDF]._
    
- **Fala durante o processamento (enquanto a barra carrega):** "O que vocês estão vendo no log é o sistema lidando com a complexidade técnica que mencionamos.
    
    - Ele está fazendo requisições concorrentes (até 10 ao mesmo tempo) para acelerar a coleta12.
        
    - Ele está lidando com falhas de rede automaticamente e garantindo que não haja dados duplicados (idempotência)13131313.
        
    - Neste momento, ele está baixando dados de deputados, despesas, partidos e votações, normalizando tudo isso para um banco de dados local14141414."
        
- **Conclusão da Demo:** "Ao finalizar, o sistema abre automaticamente o dashboard no navegador." _[Mostrar o Dashboard aberto na tela]._
    

#### **Slide 5: Detalhes da Arquitetura (Explicando o que aconteceu)**

**(Tempo estimado: 1.5 min)**

- **Visual:** Diagrama de Arquitetura (Figura 1 do PDF).
    
- **Fala Sugerida:** "O que aconteceu nos bastidores dessa demonstração segue esta arquitetura:
    
    1. Temos um **Módulo de Coleta** em Python que faz o trabalho pesado de buscar dados na API da Câmara15.
        
    2. Esses dados são limpos e salvos em um banco **SQLite** local. Escolhemos SQLite pela portabilidade, pois não exige que o usuário instale um servidor de banco de dados complexo16.
        
    3. Por fim, uma **API Local** leve serve esses dados para a interface que acabamos de ver17171717. Essa separação é crucial: permite que, no futuro, a interface mude sem quebrar a coleta de dados."
        

#### **Slide 6: Visualização e Modelo de Dados**

**(Tempo estimado: 1 min)**

- **Visual:** Diagrama do Banco (Figura 2) ou Print do Gráfico (Figura 4).
    
- **Fala Sugerida:** "O resultado para o cidadão comum são visualizações imediatas, como o gráfico de 'Top Deputados por Gasto' que vimos18181818.
    
- Porém, o maior valor para pesquisadores e jornalistas está no **Banco de Dados**. Entregamos tabelas relacionais prontas — ligando Deputados, Partidos, Despesas e Votos 191919191919191919— eliminando a etapa custosa de limpeza de dados para quem quer fazer análises mais profundas com ferramentas de Business Intelligence (BI)20202020."
    

#### **Slide 7: Conclusão e Trabalhos Futuros**

**(Tempo estimado: 1.5 min)**

- **Fala Sugerida:** "Concluindo, esta Prova de Conceito valida que é possível encapsular a engenharia de dados em uma ferramenta acessível21.
    
- Nós reduzimos a barreira técnica inicial para o controle social22.
    
- **Limitações e Futuro:** Como limitações, o uso do SQLite pode ser um gargalo para volumes massivos de dados históricos23.
    
- Como trabalhos futuros, planejamos conectar essa API local diretamente a ferramentas de BI (como PowerBI ou Metabase), permitindo que o usuário crie seus próprios relatórios dinâmicos, superando a rigidez do dashboard estático atual24.
    
- Obrigado pela atenção."
    

---

### Dicas Adicionais para a Apresentação:

1. **Durante a Demo:** Se o processamento demorar um pouco mais que o esperado (falha de rede, etc.), tenha o "Slide 5 (Arquitetura)" na manga para explicar _enquanto_ o software roda, para não ficar em silêncio.
    
2. **Sobre o Público:** Lembre-se que é um evento universitário. Enfatize que o código é aberto (Open Source) e está no GitHub, convidando a colaboração acadêmica25252525.
    
3. **Termos Técnicos:** Ao falar "ETL" ou "Idempotência", explique brevemente ou use o contexto para deixar claro, garantindo que todos na sala entendam, mesmo quem não é de Computação.