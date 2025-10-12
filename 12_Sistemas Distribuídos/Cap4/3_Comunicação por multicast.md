
O multicast permite a um processo enviar uma única mensagem para um **grupo de processos**. É importante notar que o multicast é uma das formas de comunicação que exibe **desacoplamento espacial**, pois o remetente não precisa conhecer a identidade dos destinatários.

### **1. Multicast IP**

O Multicast IP oferece um serviço de datagrama não confiável (semelhante ao UDP) de um para muitos.

- **Grupos de Multicast:** O Multicast IP utiliza o conceito de grupos de multicast. Um grupo de multicast é um conjunto de processos que se deseja que recebam cópias de uma mensagem enviada para o grupo.

• **Volatilidade do Grupo:** Os membros de um grupo de multicast podem mudar dinamicamente. Os processos podem entrar ou sair de um grupo a qualquer momento, e a adesão ao grupo não é controlada ou restrita, a menos que o grupo esteja dentro de um bloco de escopo administrativo, que restringe a propagação do tráfego multicast.

• **Grupos Permanentes:** Existem grupos de multicast permanentes, como 224.0.1.1, que é reservado para o protocolo NTP (Network Time Protocol), conforme detalhado no Capítulo 14. O intervalo de 224.0.6.000 a 224.0.6.127 é reservado para o projeto ISIS (discutido nos Capítulos 6 e 18).

Bloco de Endereços Multicast:

Os endereços multicast são divididos em blocos com propósitos específicos:

• **Bloco de controle de rede local** (224.0.0.0 a 224.0.0.225): Usado para tráfego multicast dentro de uma rede local específica.

• **Bloco de controle de Internet** (224.0.1.0 a 224.0.1.225).

• **Bloco de controle ad hoc** (224.0.2.0 a 224.0.255.0): Usado para tráfego que não se encaixa em nenhum outro bloco.

• **Bloco de escopo administrativo** (239.0.0.0 a 239.255.255.255): Usado para implementar o escopo do tráfego multicast (restringindo a propagação).

4.4.2 Programação com Multicast IP

A API para Multicast IP é baseada em soquetes e é muito semelhante à API do UDP, mas utiliza um objeto **MulticastSocket** (na API Java) que permite que um host se junte ou saia de um grupo.

• **Entrada no Grupo (Joining):** Um host deve ingressar no grupo para receber mensagens enviadas ao endereço de multicast desse grupo.

• **Envio (Sending):** Um processo envia uma mensagem para o grupo fornecendo o endereço de multicast e um número de porta para um objeto `DatagramPacket`.

O Multicast IP é usado em sistemas que precisam disseminar informações para um grande número de destinatários, como o **NTP** (Network Time Protocol), ou em sistemas que requerem alta velocidade de comunicação, como a distribuição de dados de mercado no setor financeiro.

4.5 Virtualização de Redes: Redes de Sobreposição (Overlay Networks)

Esta seção, que é **nova** na 5ª edição do livro, introduz as redes de sobreposição e é seguida por um estudo de caso sobre o Skype.

As redes de sobreposição são implementadas como uma **camada de software que roda em cima da rede de nível de rede** (por exemplo, IP) e fornecem um conjunto de funcionalidades que a rede subjacente não oferece ou que precisam ser adaptadas para aplicações específicas.

• **Modelo Conceitual:** Uma rede de sobreposição implementa um mecanismo de roteamento na camada de aplicação que é **completamente separado** de outros mecanismos de roteamento (como o roteamento IP).

• **Uso em Sistemas Peer-to-Peer:** As redes de sobreposição são amplamente utilizadas como middleware em sistemas **peer-to-peer ( em cima da rede de nível de rede** (por exemplo, IP) e fornecem um conjunto de funcionalidades que a rede subjacente não oferece ou que precisam ser adaptadas para aplicações específicas.

• **Modelo Conceitual:** Uma rede de sobreposição implementa um mecanismo de roteamento na camada de aplicação que é **completamente separado** de outros mecanismos de roteamento (como o roteamento IP).

• **Uso em Sistemas Peer-to-Peer:** As redes de sobreposição são amplamente utilizadas como middleware em sistemas **peer-to-peer (P2P)** para localizar nós e objetos, assumindo a responsabilidade por direcionar requisições de clientes para o host que contém o objeto endereçado.

• **Impacto na Arquitetura:** A introdução das redes de sobreposição tem um impacto significativo na visão conceitual da Internet para o programador, pois adiciona uma camada de funcionalidade de roteamento e endereçamento sobre o IP existente.

Estudo de Caso: Skype

O Skype é um dos **novos estudos de caso** apresentados na 5ª edição. Embora os detalhes de sua arquitetura não estejam totalmente revelados nos excertos, o Skype é mencionado no contexto da virtualização de rede, implicando que ele usa uma rede de sobreposição para conectar seus usuários.

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