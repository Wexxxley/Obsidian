
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
    - Altamente particionáveis e permitem escalonamento horizontal em um nível que outros bancos de dados tnão alcancem. Oferecem acesso de baixa latência e são ideais para operações rápidas de leitura e escrita.
    - **Casos de uso:** Caches, sessões de usuário, jogos, tecnologia de publicidade.
    - **Exemplo:** Redis.
2. **Document Databases:**
    - Armazenam dados em documentos semi-estruturados, geralmente em formato JSON. Cada documento pode ter uma estrutura diferente, permitindo que o esquema evolua com as necessidades da aplicação.
    - Permitem aninhar informações de formatos diferentes, tornando-os flexíveis para lidar com dados que mudam frequentemente.
    - **Exemplo:** MongoDB.
    - **Casos de uso:** Catálogos de produtos, perfis de usuários, blogs
    .
3. **Column-Family Databases:**
    - Armazenam dados em famílias de colunas, que são grupos de colunas relacionadas. Embora parecidos com o modelo relacional, não trabalham com tabelas rígidas. Eles são otimizados para operações de escrita rápida e para lidar com grandes volumes de dados esparsos.
    - **Características:** Gerenciam grandes volumes de dados com simplicidade e velocidade. São distribuídos e altamente escaláveis.
    - **Exemplos:** Apache Cassandra, Apache HBase.
    - **Casos de uso:** Big Data, análise de dados em tempo real

4. **Graph Databases:**    
    -  Representam os dados como um grafo, onde os **nós** representam entidades (pessoas, locais, produtos) e as **arestas** representam as conexões entre essas entidades. Cada nó e aresta pode ter propriedades.
    - **Características:** Ideais para dados altamente conectados.
    - **Exemplos:** Neo4j, Amazon Neptune, OrientDB.
    - **Casos de uso:** Redes sociais, sistemas de recomendação.
