
#Concluded 

---
==A camada de aplicação é a camada onde residem as aplicações de rede e seus respectivos protocolos. Esta camada é focada na interação direta com o software que o usuário utiliza.== 

Os protocolos de aplicação são implementados via software apenas nos **sistemas finais**. Eles não residem nos dispositivos do núcleo da rede.
### **1. Cliente x Servidor**

==Um ou mais clientes se conectam a um servidor, que é responsável por fornecer serviços ou recursos.==

- Os clientes fazem requisições, e o servidor responde. ==O servidor não deve iniciar a comunicação com o cliente.==
- Clientes não se comunicam diretamente.

### **2. Ponto-a-Ponto (Peer-to-Peer, ou P2P)**

==Cada dispositivo na rede pode agir tanto como cliente quanto como servidor. Ou seja, os usuários compartilham dados entre si diretamente.==

- Não há um servidor central. Se um nó cair, os outros continuam.
- Usa melhor os recursos da rede como um todo.
- Menor custo com infraestrutura central.
- Mais difícil de gerenciar a segurança e o controle.
 
### **3. Híbrida (Cliente-Servidor + P2P)**

Combina as duas abordagens: ==existe um servidor para organizar para descobrir ou localizar as conexões, mas a transferência de dados podem ser feitas diretamente entre os clientes.==

- O servidor organiza ou autentica os pontos.
- A comunicação entre os peers é direta.
- Combina o melhor dos dois mundos: controle e descentralização.
