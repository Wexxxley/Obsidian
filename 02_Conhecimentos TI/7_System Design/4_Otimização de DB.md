


---

OTIMIZAÇÃO DE DB
Caso base, um unico servidor, um unico db

quando o serviço chegar em muitos users naturalmente ele vai ficar lento. muitos podem pensar em criar um cache (redis), e faz sentido

se a cache n der conta:
1. Faz sentido criar replicas de leitura? (consistencia ou disponibilidade)(leitrua é mais comum, mas existe sistemas onde a escrita é mais comum?)
2. Indices no db ajudaria? faz sentido somente quando um campo é muito buscado (quais os difernetes tipos e quais os casos de uso) e os pontos negativos(escrita mais lenta, armazenamento)?
3. normalização denormalização. quando fazer e quais vantagens e desvantagens
4. ou sharding faz mais sentido? traz bem mais complexidade, queries complexas
5. connecction polling (já é o padrão?)
6. Otimização de queries
7. materialized view (pontos negativos, quando faz sentido?)
8.  Batching e pagination

- Estretegias para priorizar leituras e escritas (escritas sao mais custosas por conta dos locks?)
- Uncomitted vs committed reads
- Locks pessimistas e otimistas

### 1. O Cenário Base 
O modelo inicial consiste em uma arquitetura monolítica, onde um único servidor de aplicação comunica-se com um único servidor de banco de dados.
- À medida que o volume de usuários aumenta, consultas que demoravam milissegundos passam a enfileirar, gerando latência e lentidão perceptível no sistema.
- **Escalonamento Vertical:** A primeira reação natural é aumentar o hardware deste servidor único. Contudo, essa abordagem possui um limite físico e um custo financeiro exponencial.
### 2. A Camada de Cache em Memória
Quando o banco de dados começa a sofrer com excesso de requisições, a implementação de uma camada de cache é a primeira estratégia de alívio. Ferramentas como o Redis operam armazenando dados chave-valor diretamente na memória RAM, que possui velocidade de leitura superior aos discos de armazenamento.
- O cache é inserido entre a aplicação e o banco de dados. Antes de executar uma consulta  no banco, a aplicação verifica se o dado já está no cache. Se estiver, a resposta é imediata.      
 - O cache mitiga problemas de leitura repetitiva, mas não resolve gargalos de escrita. Todas as novas inserções e atualizações ainda precisam ser processadas e persistidas pelo banco de dados principal. 
### 3. Réplicas de Leitura (Read Replicas)
Quando os padrões de consulta são muito dinâmicos e impossíveis de serem armazenados em memória previamente, a arquitetura evolui para a replicação do banco de dados.
- **Sistemas Orientados a Leitura vs. Escrita:** A adoção de réplicas faz sentido técnico porque a vasta maioria das aplicações web (e-commerces, redes sociais, portais) possui uma carga  de leituras maior. Contudo, existem sistemas onde a escrita é dominante, como sistemas de agregação de logs de servidores e algoritmos de rastreamento financeiro de alta frequência.
- **Separação de Responsabilidades:** Cria-se um nó primário exclusivo para operações de escrita e nós secundários que processam as operações de leitura.
### 4. Indexes
A criação de índices é a técnica mais direta para reduzir o tempo de latência de consultas de leitura. Um índice é uma estrutura de dados anexa à tabela que armazena referências para os registros, permitindo que o motor do banco localize a informação sem precisar varrer todas as linhas do disco físico
- Índices são justificados em colunas que atuam como chaves de busca frequentes usados.

- **B-Tree (Árvore Balancea:** É o índice padrão em bancos de dados relacionais. Utilizado para consultas de correspondência exata ou verificações de intervalos (maior que, menor que).      
- **Hash:** Estrutura otimizada para buscas de correspondência exata.

- **Penalidade de Escrita:** Toda vez que um registro é inserido, atualizado ou excluído, o banco de dados é forçado a atualizar não apenas a tabela principal, mas também recalcular e reorganizar todos os índices associados. 
- **Custo de Armazenamento:** Índices são cópias estruturadas dos dados e, portanto, consomem volume substancial de disco.
### 5. Normalização e Desnormalização
O modelo relacional exige que os dados sejam modelados para evitar redundâncias, mas essa premissa pode se tornar um gargalo de performance em cenários de alto tráfego.

- **Normalização:** É o processo de dividir os dados em múltiplas tabelas interligadas por chaves estrangeiras, eliminando informações duplicadas.
    - **Vantagem:** Garante integridade referencial absoluta. Otimiza o armazenamento, pois evita repetição de dados.
    - **Desvantagem:** Para construir a visualização de um dado completo para o usuário, o banco de dados precisa executar junções complexas de múltiplas tabelas (_JOINs_).
- **Desnormalização:** É a quebra intencional das regras de normalização. Consiste em reinserir dados redundantes em uma tabela para evitar a execução de _JOINs_.
    - **Vantagem:** Reduz drasticamente o tempo de leitura.
    - **Desvantagem:** Se uma informação replicada precisar ser alterada, o sistema deverá atualizá-la em múltiplos registros simultaneamente.

### 6. Sharding (Fragmentação Horizontal)
O banco de dados é dividido matematicamente, e os registros (linhas da tabela) são espalhados por múltiplos servidores físicos autônomos. O _sharding_ é o último recurso de escalabilidade. É adotado quando o limite físico de hardware (_CPU/RAM/Disco_) foi atingido e o sistema continua apresentando colapsos sob a carga de inserções simultâneas.
[3_Partition e Read Replics](3_Partition%20e%20Read%20Replics.md)
### 7. Connection Pooling
Abrir e fechar uma conexão com um banco de dados é uma operação cara, pois envolve a resolução de rede (TCP/IP), o aperto de mãos de segurança (_Handshake_ SSL/TLS) e a alocação de memória no servidor.

O _Connection Pooling_ mantém um conjunto (pool) de conexões já abertas e ativas em memória. Quando a aplicação precisa executar uma consulta, ela empresta uma conexão do _pool_, executa a operação e a devolve, sem a necessidade de fechar o canal.

Praticamente todos os ecossistemas de desenvolvimento utilizam _Connection Pooling_ de forma nativa e habilitada por padrão.
### 8. Otimização de Queries

A otimização em nível de código consiste em garantir que o motor do banco de dados execute o menor esforço possível para retornar a informação.

- **Seleção Estrita:** Evita-se selecionar tudo: `SELECT *`. Deve-se especificar as colunas estritamente necessárias.
- **Prevenção do Problema N+1:** Evita-se arquiteturas onde a aplicação faz uma consulta inicial para buscar uma lista de entidades e, em seguida, executa uma nova consulta no banco para cada entidade individual iterada em um laço de repetição.
### 9. Materialized Views 

Uma Materialized View é a execução prévia de uma consulta altamente complexa, cujo resultado final é salvo fisicamente no disco rígido do banco de dados.

É a estratégia ideal para a geração de relatórios financeiros mensais, painéis de controle analíticos e sumarizações de dados históricos onde a visualização imediata não exige informações atualizadas no exato segundo da requisição. Os dados tornam-se obsoletos. A visão materializada precisa ser atualizada periodicamente 
### 10. Batching e Paginação

- **Batching:** Em vez de enviar mil comandos de inserção separados, a aplicação agrupa os dados e os envia em uma única requisição e em uma única transação de rede. Isso reduz drasticamente a latência de comunicação e o esforço de escrita (I/O) do banco de dados.
- **Paginação:** É a técnica de segmentar o retorno de dados volumosos em blocos menores (usando cláusulas como `LIMIT` e `OFFSET` ou cursores lógicos).
### 11. Estratégias de Leituras vs. Escritas e o Custo dos Locks

- **O Custo da Escrita:** A lentidão não ocorre apenas pela persistência física no disco rígido, mas também pela necessidade de reordenar todos os índices secundários associados àquela tabela e validar restrições de integridade.
- **A Sobrecarga dos Bloqueios (Locks):** Para garantir a propriedade de Isolamento das transações (ACID), o banco de dados aplica bloqueios sistêmicos nos registros que estão sendo alterados.
### 12. Uncommitted vs. Committed Reads

- **Read Uncommitted:** A aplicação recebe permissão para ler dados que estão no meio de uma transação aberta de outro usuário, mas que ainda não foram confirmados.
    - O usuário lê um dado que pode ser cancelado (_Rollback_) pela outra transação um milissegundo depois, fazendo com que a aplicação opere baseada em uma informação que oficialmente nunca existiu no sistema.
- **Read Committed:** É o padrão na maioria dos bancos relacionais. A aplicação só consegue enxergar dados que já foram permanentemente salvos.
### 13. Locks Pessimistas vs. Otimistas

- **Lock Pessimista:** A arquitetura parte da premissa de que o conflito ocorrerá. Assim que a primeira requisição inicia a leitura com a intenção de atualizar, o banco de dados bloqueia a linha. Nenhuma outra requisição pode ler ou alterar aquele registro até que a transação inicial termine. É seguro, porém gera retenção de performance em sistemas 
    
- **Lock Otimista:** A arquitetura parte da premissa de que o conflito é raro. Nenhum bloqueio é aplicado no banco de dados. Em vez disso, a tabela possui uma coluna de versão (ou _timestamp_). A aplicação lê o dado (Versão 1). No momento da atualização, ela instrui o banco: "Atualize este dado, mas apenas se a versão ainda for a 1". Se outro usuário já tiver alterado para a Versão 2 no meio do processo, a operação é rejeitada e a aplicação decide se tenta novamente ou exibe um erro para o usuário. Permite alta concorrência e melhor escalabilidade sem o custo de bloqueios travando o banco.