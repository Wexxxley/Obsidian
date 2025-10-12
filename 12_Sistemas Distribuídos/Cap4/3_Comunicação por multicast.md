
O multicast permite a um processo enviar uma única mensagem para um **grupo de processos**. É importante notar que o multicast é uma das formas de comunicação que exibe **desacoplamento espacial**, pois o remetente não precisa conhecer a identidade dos destinatários.

### **1. Multicast IP**

O Multicast IP oferece um serviço de datagrama não confiável (semelhante ao UDP) de um para muitos.

- **Grupos de Multicast:** O Multicast IP utiliza o conceito de grupos de multicast. Um grupo de multicast é um conjunto de processos que se deseja que recebam cópias de uma mensagem enviada para o grupo.

- **Volatilidade do Grupo:** Os membros de um grupo de multicast podem mudar dinamicamente. Os processos podem entrar ou sair de um grupo a qualquer momento, e a adesão ao grupo não é controlada ou restrita, a menos que o grupo esteja dentro de um bloco de escopo administrativo, que restringe a propagação do tráfego multicast.

O Multicast IP é usado em sistemas que precisam disseminar informações para um grande número de destinatários, como o **NTP** (Network Time Protocol), ou em sistemas que requerem alta velocidade de comunicação, como a distribuição de dados de mercado no setor financeiro.

---
### 2. Redes de Sobreposição (Overlay Networks)

Uma **rede de sobreposição (overlay)** é uma rede virtual construída sobre uma rede subjacente já existente, como a Internet. Essa rede virtual é composta por seus próprios nós e enlaces virtuais, e seu objetivo é oferecer funcionalidades que a rede de base não fornece.

#### Principais Características e Vantagens:

- **Serviços Personalizados**: Elas permitem a criação de serviços de rede customizados para as necessidades de uma aplicação específica ou para fornecer um recurso adicional, como comunicação por multicast ou comunicação segura.
    
- **Extensibilidade e Experimentação**: Tornam possível definir e experimentar novos serviços de rede sem a necessidade de modificar a rede subjacente, o que é crucial dada a complexidade e padronização da Internet.
#### Desvantagens:

- **Sobrecarga de Desempenho**: A introdução de um nível extra de indireção pode acarretar uma queda no desempenho.
    
- **Aumento da Complexidade**: Elas aumentam a complexidade dos serviços de rede quando comparadas à arquitetura mais simples da rede TCP/IP subjacente.

#### Funcionamento:
As redes de sobreposição funcionam de maneira análoga às camadas lógicas, mas operam fora da pilha de protocolos padrão (como TCP/IP). Isso dá aos desenvolvedores a liberdade de redefinir elementos fundamentais da rede, como:

- **Modo de Endereçamento**: Podem criar esquemas de endereçamento próprios.
    
- **Protocolos**: Podem empregar protocolos específicos para a aplicação.
    
- **Estratégia de Roteamento**: Podem introduzir estratégias de roteamento radicalmente diferentes, como o **roteamento baseado em chave** usado em tabelas de hash distribuídas (DHTs).



4.6 Estudo de Caso: MPI (Message Passing Interface)

O MPI (Interface de Passagem de Mensagens) é outro **novo tópico** introduzido nesta edição. Esta seção examina como a passagem de mensagens é oferecida para um conjunto de processos (ou _threads_) em um sistema distribuído, oferecendo mais controle e opções do que as primitivas de soquetes padrão.

• **Contexto:** O MPI é tipicamente usado para a **computação paralela** de alto desempenho (HPC), onde a ênfase é colocada na coordenação eficiente entre os processos.

• **Primitivas** **send** **e** **receive****:** O MPI refina a visão básica da passagem de mensagens, separando a semântica de passagem de mensagens em dimensões síncronas/assíncronas e com bloqueio/sem bloqueio.

Variantes da Operação no MPI:

A operação `send` é definida em várias variantes, sendo que o ponto crucial para o bloqueio é a garantia de que o **buffer do aplicativo possa ser reutilizado**.

|   |   |   |
|---|---|---|
|Categoria|Operação MPI|Descrição|
|**Genéricas (Bloqueantes)**|`MPI_Send`|O remetente bloqueia até que seja seguro retornar (a mensagem está em trânsito ou foi entregue). Na prática, frequentemente implementado como `MPI_Ssend`.|
|**Síncronas**|`MPI_Ssend`|O remetente e o destinatário são **sincronizados**; a chamada retorna **somente quando a mensagem tiver sido entregue** no endereço do destinatário. Corresponde à passagem de mensagens síncrona e com bloqueio.|
|**Prontas**|`MPI_Rsend`|Retorna quando o buffer pode ser reutilizado (como `MPI_Send`), mas o programador **indica que o destinatário está pronto** para receber, o que pode otimizar a implementação subjacente.|
|**Não Bloqueantes**|`MPI_Isend`|A chamada retorna **imediatamente**. O programador recebe um identificador de pedido de comunicação, que deve ser usado para verificar o andamento da chamada posteriormente via `MPI_Wait` ou `MPI_Test`.|
||`MPI_Irsend`|Efeito igual ao de `MPI_Isend`, mas indica que o destinatário está pronto, permitindo otimizações.|

**MPI e Bloqueio:** Para as operações de bloqueio, "bloqueado" significa que o processo (ou _thread_) fica suspenso até que os dados do aplicativo tenham sido copiados com segurança para o ambiente MPI (ou entregues), permitindo a reutilização do buffer do aplicativo. Na comunicação assíncrona, a operação `send` é tipicamente **não bloqueante**, permitindo que o processo prossiga enquanto a transmissão ocorre em paralelo.

Aguarde o comando `next` para continuarmos a discussão do material de apoio.