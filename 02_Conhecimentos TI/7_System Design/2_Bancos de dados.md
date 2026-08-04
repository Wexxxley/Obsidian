


---

Banco de dados são sistemas utilizados para armazenar, administrar e recuperar dados. São eficientes, robustos e oferecerem escalabilidade.
### 1. Bancos de Dados SQL 
Os dados são organizados em tabelas e possuem formato estruturado.Indicados para domínios que exigem alta confiabilidade de dados e buscas complexas, como instituições financeiras e marketplaces.
- **Schema-on-Write:** O banco verifica ativamente se o formato recebido pelo cliente coincide com o formato tipado da coluna na tabela.
- **ACID:**  Propriedades essenciais de uma transação de banco de dados confiável. [7_ACID](../../01_Concursos/TI/03_Banco%20de%20dados/1_Relacional/7_ACID.md)
### 2. Bancos de Dados NoSQL
Apresentam Schema flexível, são otimizados para alto **throughput** (capacidade de processar um volume massivo de requisições de leitura e escrita) e facilitam a escalabilidade horizontal. Indicados para sistemas de registro de Logs, para armazenamento em Cache, etc.

**Impedance Mismatch**: Em sistemas relacionais, há uma dificuldade estrutural em pegar um objeto de código (com listas e objetos aninhados) e tratá-lo para caber em tabelas bidimensionais. Bancos de dados NoSQL, especialmente os baseados em documentos, costumam mitigar esse problema, pois o dado é salvo no banco de forma estruturalmente idêntica a como ele existe na memória do software.

- **Chave Valor:** Focados em recuperação ultrarrápida através de uma chave única (Redis).
- **Documentos:** Armazenam dados em formatos hierárquicos, como JSON, permitindo aninhar informações (MongoDB).
- **Grafos:** Focados em mapear relacionamentos e conexões complexas que podem ser representadas como grafos (Neo4j).
- **Vetores:** Armazenam dados como coordenadas matemáticas, essenciais para sistemas de recomendação e Inteligência Artificial (Pinecone).

