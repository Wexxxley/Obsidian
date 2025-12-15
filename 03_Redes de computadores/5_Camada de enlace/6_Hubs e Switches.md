
#Concluded 

---
### **Hub**
Um hub opera na **Camada 1 (Física)**. Um hub é basicamente um repetidor de sinais elétricos. Ele não "entende" os dados da mesma forma que um switch ou roteador.
- **Broadcast**: Quando um bit chega a uma das portas do hub, ele é imediatamente copiado e enviado para _todas_ as outras portas conectadas
- **Um hub não faz conversão de velocidade**.
- **Não possuem armazenagem de quadros.** Ao contrário de um switch, um hub não tem memória para armazenar quadros de dados.
- É importante entender que o mecanismo **CSMA/CD** não é implementado _dentro_ do hub. Em vez disso, a detecção e o tratamento de colisões ocorrem nos **adaptadores de rede** de cada dispositivo final conectado ao hub. 
- **Domínio de colisão**: Um "domínio de colisão" é uma área da rede onde as colisões de dados podem ocorrer. Como um hub simplesmente retransmite tudo para todos, todos os dispositivos conectados a um hub fazem parte de um **único e grande domínio de colisão**.

![Pasted image 20250702154313](../../attachments/Pasted%20image%2020250702154313.png)

---
### **Switch**
Um switch é um **dispositivo de camada de enlace**. Diferente dos hubs, os switches são capazes de "entender" e processar os quadros Ethernet.
- **Armazena e encaminha quadros Ethernet:** Ao receber um quadro de dados, o switch o armazena temporariamente antes de tomar uma decisão de encaminhamento.
- **Unicast**: Um switch lê o **end MAC** de destino e encaminha o quadro apenas para a porta específica. Isso cria segmentos, onde cada porta se torna um domínio de colisão individual.
- **Transparente:** Isso significa que os computadores conectados à rede não "percebem" a presença do switch; Não há necessidade de configuração.
- **Full-duplex**. [5_Modos de transmissão de dados](../1_Introdução/5_Modos%20de%20transmissão%20de%20dados.md)

![400](../../attachments/Pasted%20image%2020250717181203.png)

A inteligência de um switch reside em sua capacidade de aprender as localizações dos dispositivos conectados a ele. Para isso, ele mantém uma **tabela**, a tabela MAC. [3_MAC e ARP](3_MAC%20e%20ARP.md)

- **Como o Aprendizado Acontece:** Quando um switch recebe um quadro ele automaticamente aprende a localização do transmissor.
- Cada entrada tem um tempo de vida, que pode ser, por exemplo, 60 minutos. Se um dispositivo não transmitir por esse período, sua entrada é removida, mantendo a tabela atualizada e eficiente.
- **ARP Request - Broadcast**: Quando o switch precisa descobrir um endereço MAC para um IP que não está em sua tabela, ele pergunta para _todos_ na rede local. 
- **ARP Reply - Unicast**: O dispositivo que possui o endereço IP alvo recebe a requisição. Como ele agora sabe o endereço MAC do remetente, ele pode enviar a **Resposta ARP** diretamente.

