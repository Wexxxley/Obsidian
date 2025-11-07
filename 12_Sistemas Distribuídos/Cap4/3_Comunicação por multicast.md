

---
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
#### Funcionamento

As redes de sobreposição dão aos desenvolvedores a liberdade de redefinir elementos fundamentais da rede para se adequarem melhor às suas aplicações. Isso inclui:
  
- **Protocolos**: Podem empregar protocolos específicos para a aplicação.
    
- **Estratégia de Roteamento**: Podem introduzir estratégias de roteamento radicalmente diferentes, como o **roteamento baseado em chave** usado em tabelas de hash distribuídas.

---
### **Estudo de Caso - Skype**

O Skype é uma aplicação peer-to-peer que oferece chamadas de voz sobre IP (VoIP), além de outros recursos como mensagens instantâneas e videoconferência.

O Skype cria uma rede virtual sobre a Internet para conectar seus usuários, permitindo chamadas sem a necessidade de conhecer endereços IP ou portas. Sua arquitetura é baseada em uma infraestrutura peer-to-peer que consiste em dois tipos de nós:

1. **Hosts Convencionais**: As máquinas normais dos usuários que estão executando o app Skype.
    
2. **Supernós**: São hosts convencionais do Skype que possuem recursos suficientes para assumir um papel mais importante na rede. Eles são selecionados dinamicamente com base nesses critérios.

![500](../../attachments/Pasted%20image%2020251012081408.png)


- **Conexão e Login**: Quando um usuário inicia o Skype, ele se autentica em um **servidor de login** centralizado e conhecido. Em seguida, o cliente se conecta a um dos **supernós**. Cada cliente mantém uma lista (cache) de supernós conhecidos para facilitar essa conexão.
    
- **Busca de Usuários**: A principal função dos supernós é gerenciar um **índice global e distribuído de usuários**. Quando você quer ligar para um amigo, seu cliente envia uma requisição para o supernó ao qual está conectado. Esse supernó, então, orquestra uma busca, consultando outros supernós até que a localização do seu amigo seja encontrada.
    
- **Conexão de Voz**: Uma vez que o usuário desejado é localizado, o Skype tenta estabelecer uma conexão de voz **diretamente entre os dois hosts (clientes)**. Ele usa o protocolo TCP para sinalizar o início e o fim da chamada, e geralmente usa o protocolo **UDP** (mais rápido, mas menos confiável) para o streaming de áudio. 

---
### **Estudo de caso - MPI**

O **MPI (Message Passing Interface)** é um padrão desenvolvido para fornecer uma API para a comunicação por **passagem de mensagens**. Ele surgiu com o objetivo de criar uma única especificação que fosse ao mesmo tempo simples, eficiente e flexível.

A verdadeira força e complexidade do MPI residem na variedade de operações que ele oferece, dando ao programador um controle extremamente fino sobre a semântica da comunicação. 

![](../../attachments/Pasted%20image%2020251012082812.png)