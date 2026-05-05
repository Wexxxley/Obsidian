
#Concluded 

___
### **1. Arquitetura TCP/IP**

Modelo abstrato que define como os componentes da rede se organizam e interagem para permitir a comunicação entre dispositivos. Essa arquitetura define um conjunto de protocolos de comunicação.
![500](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfm0yiF7VCzT2a3-JAYru0-quEMlNGUffyxN3fS5Fw5FcE-dLzkcmRKVMUy9w_TElxVHpZoiixrmQQvHFQSTNLnfufA9-vIj1QFtH5j-5k5OO6kciHH31tXXDk5hjJlJ5ULqPUS?key=HrOhHC0_-ked6RNCpQ0o3PZn)

1. **Aplicação:** Contém os protocolos usados pelos softwares que os usuarios interagem.
2. **Transporte:** Cuida da entrega dos dados entre dois dispositivos. Responsável pela confiabilidade (TCP) ou velocidade (UDP). 
3. **Rede:** Roteia os pacotes IP até o destino. 
4. **Enlace:** Transferência de dados entre elementos vizinhos de rede.
5. **Física:** Converte os bits em sinais elétricos, ondas ou luz. 

**IP(Internet protocol):** É o <mark style="background: #ADCCFFA6;">protocolo (Camada de rede) responsável por endereçar e encaminhar os pacotes na rede. Ele não garante que os dados cheguem corretamente ou na ordem certa. Só se preocupa em levar o pacote</mark>.

**TCP (Transmission Control Protocol):** Protocolo (Camada de transporte) que <mark style="background: #ADCCFFA6;">cuida da confiabilidade da comunicação e garante que os dados cheguem completos, na ordem correta, sem duplicação e sem perda</mark>.  
