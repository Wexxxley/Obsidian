

---
#### **1. Abertura**
**(Tempo estimado: 1 min)**

- "Olá a todos. Me chamo Wesley e, juntamente com meu colega George, desenvolvemos o projeto **'Ferramenta para Extração e Visualização de Dados Parlamentares'**.

- Este projeto apresenta uma prova de conceito (POC) de uma arquitetura de software integrada, distribuída como um aplicativo, projetada para simplificar a coleta, tratamento, armazenamento e a análise de dados abertos da Câmara dos Deputados.

 - Lembrando que o projeto é de código aberto.
#### **2. A Problematização**
**(Tempo estimado: 2 min)**

- Vivemos hoje numa era de 'dilúvio de dados'. Embora a transparência governamental seja essencial e existam portais como o da Câmara dos Deputados que oferecem um volume massivo de informações, existem barreiras:
    
    - A mera existência do dado não garante transparência.
    - Para o cidadão comum, e até para jornalistas, os dados estão fragmentados em formatos heterogêneos como JSON, XML e CSV.
    - As infomações estão separadas em locais e com métodos de acesso diferentes.
    - Sem conhecimento em programação para consumir APIs complexas, o cidadão não consegue transformar esses dados em informação útil. É aqui que nosso trabalho atua.

- Nós criamos uma ferramenta que automatiza o processo de ETL (_Extract, Transform, Load_), entregando ao usuário final gráficos prontos e, ao pesquisador, um banco de dados limpo e estruturado.

#### **3. Demonstração Prática**
**(Tempo estimado: 2 min)**

- Vou demonstrar a execução da ferramenta agora. Como se trata de uma Prova de Conceito, focamos na facilidade de distribuição. O usuário seleciona o ano desejado — vamos usar 2022 como exemplo — e inicia o processamento.
#### **4. Detalhes da Arquitetura**
**(Tempo estimado: 1.5 min)**

1. Temos um **Módulo de Coleta** em Python que faz o trabalho pesado de buscar dados na API da Câmara.
	
2. Esses dados são limpos e salvos em um banco **SQLite** local. Escolhemos SQLite pela portabilidade, pois não exige que o usuário instale um servidor de banco de dados complexo.
	
3. Por fim, uma API Local leve serve esses dados para a interface que acabamos de ver. Essa separação permite que, no futuro, a interface mude sem quebrar a coleta de dados.

#### **5. Visualização e Modelo de Dados**

- O resultado para o cidadão comum são visualizações imediatas.
    
- Porém, o maior valor para pesquisadores e jornalistas está no **Banco de Dados**. Entregamos tabelas relacionais prontas, eliminando a etapa custosa de limpeza de dados para quem quer fazer análises mais profundas com ferramentas de Business Intelligence (BI)"

#### **6. Conclusão**
**(Tempo estimado: 1.5 min)**

- Concluindo, esta Prova de Conceito valida que é possível encapsular a engenharia de dados em uma ferramenta acessível.
    
- **Limitações:** Como limitações, o uso do SQLite pode ser um gargalo para volumes massivos de dados históricos. Como trabalhos futuros, seria interessante conectar essa API local diretamente a ferramentas de BI, permitindo que o usuário crie seus próprios relatórios dinâmicos, superando a rigidez do dashboard estático atual.
