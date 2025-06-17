
---

### **1. SQL vs noSQL**
**Pontos negativos de SGDB's SQL**
- Certos tipos de dados são complicados de guardar no schema, por exemplo um json pode ter que ser fragmentado e armazenado em várias tabelas.
- Escalabilidade vertical, chega um ponto que não da para melhorar mais o servidor, e escalar horizontalmente bando de dados relacionais é complicado.

**Vantagens noSQL**
- Os bancos NoSQL não exigem a definição de um esquema fixo. Isso permite que diferentes registros em uma mesma coleção armazenem dados com formatos variados.

- ○ Bancos NoSQL são projetados para crescer adicionando mais servidores (escalabilidade horizontal), ao contrário dos bancos relacionais que frequentemente dependem de hardware mais robusto (escalabilidade vertical).

- Os bancos NoSQL suportam diferentes modelos de dados, como documentos, chave-valor, colunares e grafos.

---
### **2. Tipos de dabases noSQL**

- 1. **Key-Value Stores:**
    - Armazenam dados como um conjunto de pares de chave-valor. O valor associado pode ser qualquer coisa, desde objetos simples até objetos compostos complexos.
    - Altamente particionáveis e permitem escalonamento horizontal em um nível que outros tipos de bancos de dados talvez não alcancem. Oferecem acesso de baixa latência e são ideais para operações rápidas de leitura e escrita.
    - **Exemplos:** Redis, Amazon DynamoDB, Riak.
    - **Casos de uso:** Caches, sessões de usuário, jogos, tecnologia de publicidade, IoT.
2. **Bancos de Dados de Documentos (Document Databases):**
    
    - **Como funcionam:** Armazenam dados em documentos flexíveis e semi-estruturados, geralmente em formato JSON (JavaScript Object Notation), BSON, XML ou YAML. Cada documento pode ter uma estrutura diferente, permitindo que o esquema evolua com as necessidades da aplicação.
    - **Características:** Permitem aninhar informações de formatos diferentes, tornando-os flexíveis para lidar com dados que mudam frequentemente. Possuem APIs intuitivas para desenvolvimento.
    - **Exemplos:** MongoDB, Amazon DocumentDB, CouchDB.
    - **Casos de uso:** Catálogos de produtos, perfis de usuários, sistemas de gerenciamento de conteúdo, blogs.
3. **Bancos de Dados de Colunas (Column-Family Databases):**
    
    - **Como funcionam:** Armazenam dados em famílias de colunas, que são grupos de colunas relacionadas. Embora parecidos com o modelo relacional, não trabalham com tabelas rígidas. Eles são otimizados para operações de escrita rápida e para lidar com grandes volumes de dados esparsos.
    - **Características:** Gerenciam grandes volumes de dados com simplicidade e velocidade. São distribuídos e altamente escaláveis.
    - **Exemplos:** Apache Cassandra, Apache HBase.
    - **Casos de uso:** Big Data, análise de dados em tempo real, sistemas de mensagens, gerenciamento de eventos.
4. **Bancos de Dados de Grafos (Graph Databases):**
    
    - **Como funcionam:** Representam os dados como um grafo, onde os **nós** (ou vértices) representam entidades (pessoas, locais, produtos) e as **arestas** (ou relacionamentos) representam as conexões entre essas entidades. Cada nó e aresta pode ter propriedades.
    - **Características:** Ideais para dados altamente conectados e para modelar e consultar relacionamentos complexos de forma intuitiva.
    - **Exemplos:** Neo4j, Amazon Neptune, OrientDB.
    - **Casos de uso:** Redes sociais, sistemas de recomendação, detecção de fraude, gerenciamento de identidade.

## Vantagens dos SGBDs NoSQL:

As principais vantagens dos SGBDs NoSQL em comparação com os SGBDs relacionais incluem:

1. **Escalabilidade Horizontal (Scale-Out):** Os bancos de dados NoSQL são projetados para escalar horizontalmente, o que significa que você pode adicionar mais servidores (nós) para distribuir a carga de trabalho e o volume de dados. Isso permite lidar com grandes volumes de dados e tráfego de usuários de forma mais eficiente do que o escalonamento vertical (aumentar o poder de processamento de um único servidor), que é mais comum em bancos de dados SQL.
    
2. **Flexibilidade de Esquema (Schema-less):** Ao contrário dos bancos de dados relacionais que exigem um esquema predefinido e rígido, os bancos de dados NoSQL oferecem esquemas flexíveis ou inexistentes. Isso é extremamente útil para lidar com dados semi-estruturados ou não estruturados, e permite que os desenvolvedores adaptem facilmente o modelo de dados às necessidades em constante mudança da aplicação, acelerando o desenvolvimento e a prototipagem.
    
3. **Alta Disponibilidade e Tolerância a Falhas:** Muitos SGBDs NoSQL são projetados com arquiteturas distribuídas, o que significa que os dados são replicados em vários nós. Se um nó falhar, outros nós podem assumir o trabalho, garantindo a alta disponibilidade do sistema.
    
4. **Desempenho Otimizado para Casos de Uso Específicos:** Cada tipo de SGBD NoSQL é otimizado para um modelo de dados específico e para certos padrões de acesso. Isso pode resultar em um desempenho superior para workloads que se encaixam nesses modelos, como operações de leitura/escrita rápidas em larga escala ou consultas complexas em grafos.
    
5. **Custo-Benefício:** Em alguns cenários, a escalabilidade horizontal dos bancos de dados NoSQL pode ser mais econômica do que o escalonamento vertical dos bancos de dados relacionais, pois permite a utilização de hardware mais comum e de baixo custo.
    
6. **Gerenciamento de Dados Não Estruturados e Semi-estruturados:** Os bancos de dados NoSQL são ideais para armazenar e gerenciar dados que não se encaixam facilmente em um formato tabular, como documentos JSON, imagens, vídeos, logs, dados de sensores IoT e dados de redes sociais.