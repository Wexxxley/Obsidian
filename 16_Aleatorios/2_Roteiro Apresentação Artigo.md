

---
#### **1. Abertura**
- "Olá a todos. Me chamo Wesley e, juntamente com meu colega George, desenvolvemos o projeto **'Ferramenta para Extração e Visualização de Dados Parlamentares'**.

- Este projeto apresenta uma prova de conceito (POC) de uma arquitetura de software integrada, distribuída como um aplicativo, projetada para simplificar a coleta, tratamento, armazenamento e a análise de dados abertos da Câmara dos Deputados.

 - Lembrando que o projeto é de código aberto.
#### **2. A Problematização**
- Vivemos hoje numa era de 'dilúvio de dados'. Embora a transparência governamental seja essencial e existam portais como o da Câmara dos Deputados que oferecem um volume massivo de informações, existem barreiras:
    
    - A mera existência do dado não garante transparência.
    - Para o cidadão comum, e até para jornalistas ou pesquisadores, os dados estão fragmentados em formatos heterogêneos como JSON, XML e CSV.
    - As infomações estão separadas em locais e com métodos de acesso diferentes.
    - Sem conhecimento em programação para consumir APIs complexas, o cidadão não consegue transformar esses dados em informação útil. É aqui que nosso trabalho atua.
#### **3. Nosso projeto**
- Nós criamos uma ferramenta que automatiza o processo de ETL (_Extract, Transform, Load_), entregando ao usuário final gráficos prontos e, ao pesquisador, um banco de dados limpo e estruturado.
#### **4. Arquitetura e banco de dados**

1. Temos um **Módulo de Coleta** em Python que faz o trabalho pesado de buscar dados na API da Câmara.
	
2. Esses dados são tratados e salvos em um banco **SQLite** local. Escolhemos SQLite pela portabilidade, pois não exige que o usuário instale um servidor de banco de dados complexo.
	
3. Por fim, uma API Local leve serve esses dados para a interface que acabamos de ver. Essa separação permite que, no futuro, a interface mude sem quebrar a coleta de dados.
#### **5. Execução**
#### **6. Conclusão**
- Este trabalho demonstrou a viabilidade de uma arquitetura que encapsula a complexidade da engenharia de dados. Ao focar na simplicidade, o projeto reduz a barreira técnica inicial.

- Como uma POC, a solução possui limitações. A escolha do SQLite é um gargalo para a escalabilidade, sendo ideal sua substituição por um Data Warehouse, que é um banco de dados projetado especificamente para **realizar análise e gerar relatórios**.

- A interface de visualização é estática. A evolução natural seria expor a API Local a ferramentas de Business Intelligence, permitindo que o usuário tenha como criar suas próprias análises dinâmicas.

