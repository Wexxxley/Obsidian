

---

Essas estretégias podem ser tanto lógicas ou físicas.
### 1. Réplicas de Leitura

Estratégia focada em escalonamento horizontal para operações de consulta. Consiste em criar cópias exatas e contínuas (somente leitura) de um banco de dados principal. O objetivo é aliviar a carga de processamento do servidor principal, direcionando o tráfego de leitura para máquinas secundárias.
![500](../../attachments/Pasted%20image%2020260805092832.png)
- **Nó Primário:** Única instância autorizada a receber requisições de mutação. 
- **Nós Secundários:** São servidores adicionais que possuem os mesmos dados do nó primário, mas configurados estritamente para receber comandos de leitura.
- **Propagação:** Sempre que uma transação de escrita é confirmada no nó primário, ele registra essa alteração em um log sequencial. O motor de replicação envia esse log pelas conexões de rede para as réplicas.
- **Roteamento:** No backend, as funções que gravam dados conectam-se ao primário, e as funções que apenas buscam informações são balanceadas entre as réplicas disponíveis.

- **Replicação Assíncrona:** O nó primário processa a gravação de dados, envia o sinal de "sucesso" imediatamente para a aplicação e, paralelamente , envia os dados às réplicas. Isso maximiza o desempenho da escrita, mas gera a "Latência de Replicação".
- **Replicação Síncrona:** O nó primário só retorna o sinal de "sucesso" para a aplicação após enviar a atualização para as réplicas e receber a confirmação de que elas também salvaram o dado. Isso garante consistência rigorosa, mas aumenta o tempo de resposta da aplicação.

 Sua adoção é justificada no seguinte cenário:
- **Read-Heavy Systems:** Sistemas onde ocorrem centenas de consultas para cada gravação de dado (como e-commerces, portais de conteúdo ou alimentação de feeds)

---
### 2. Particionamento

Processo de dividir um banco de dados em partes menores. Pode ser local ou distribuído. O objetivo é otimizar o tempo de varredura das consultas, reduzir o tamanho dos índices.

- **Particionamento Vertical:** Separar colunas ou tebalas -> de acordo com a RESPONSABILIDADE
	![300](../../attachments/Pasted%20image%2020260805094119.png)
- **Particionamento Horizontal:** Separar linhas/registros de uma mesma tabela.
	![300](../../attachments/Pasted%20image%2020260805094355.png)

**Sharding**: Sharding é uma implementação do particionamento horizontal desenhada especificamente para sistemas distribuídos. 
- **Autonomia dos Nós:** Cada shard opera como um banco de dados autônomo, processando suas próprias gravações e leituras de forma independente. 
- **Shard Key:** Para gerenciar o roteamento de dados na rede, a arquitetura exige uma chave de fragmentação. Trata-se de um valor ou algoritmo de dispersão (hash) aplicado a um atributo do dado. O resultado desse cálculo aponta para o endereço físico do servidor que contém aquela informação específica.
- **Key-range:** abordagem mais simples, cada db tem um range definido. Pode gerar HotSpots e necessidade de balanceamento constante.
- **Diferença**: O particionamento resolve o esgotamento de recursos internos de um servidor único, otimizando o escalonamento vertical. O sharding é o mecanismo fundamental do escalonamento horizontal, permitindo que a capacidade do banco de dados cresça de forma praticamente ilimitada mediante a adição de novos servidores físicos ao cluster.

---
### 4. Índice Secundário

Quando um banco de dados opera sob a arquitetura sharding, a distribuição física dos registros entre os servidores é governada por um atributo eleito como a Chave de Fragmentação. Se a aplicação realizar uma consulta filtrando por um atributo diferente, como o nome, o sistema distribuído enfrenta um conflito de roteamento.

**Scatter-Gather:** Se a busca ocorre pelo nome, o roteador não possui um mapeamento  que vincule esse texto a um servidor. Para encontrar, o roteador é forçado a enviar a consulta para todos os servidores. Cada servidor executa a busca e devolve os resultados encontrados. 

**Índices Secundários Globais**: Para viabilizar consultas eficientes por atributos que não são a chave primária, bancos de dados distribuídos (especialmente os NoSQL) utilizam uma estrutura denominada Índice Secundário Global.

Na prática, funciona como uma nova tabela particionada. Nesta estrutura, o atributo de busca atua como a nova Shard Key, enquanto o valor armazenado é apenas o ID original Quando a aplicação busca por um nome, o roteador calcula o hash desse nome, consulta o servidor responsável para descobrir o ID correspondente, e então busca o dado completo.

- **Duplicação de Armazenamento:** Manter GSIs exige que o banco de dados replique os dados ou crie extensas tabelas de referência.
- **Consistência:** Quando a aplicação insere ou atualiza um registro, o banco de dados precisa gravar o dado no nó primário e, simultaneamente, trafegar pela rede para atualizar o índice secundário em outro nó. Isso aumenta o tempo de resposta da escrita e obriga o sistema a adotar a **Consistência Eventual**.

---
### 5. Cold Storage

Estratégia focada no arquivamento de informações inativas ou de acesso extremamente raro. Em contraste com os dados quentes (_Hot Data_), que são consultados e alterados constantemente pela aplicação em tempo real, os dados frios (_Cold Data_) englobam históricos antigos, registros de logs estáticos, transações consolidadas e backups retidos por exigência de conformidade legal. A recuperação de uma informação armazenada nesta infraestrutura pode demorar de vários minutos até horas.
