
---

Um hub opera na **Camada 1 (Física)**. Um hub é basicamente um repetidor de sinais elétricos. Ele não "entende" os dados da mesma forma que um switch ou roteador.

- **Broadcast**: Quando um bit chega a uma das portas do hub, ele é imediatamente copiado e enviado para _todas_ as outras portas conectadas. Isso significa que todos os dispositivos conectados ao hub recebem cada bit de dados transmitido por qualquer outro dispositivo no mesmo hub.
- **Um hub não faz conversão de velocidade**.
- **Não possuem armazenagem de quadros.** Ao contrário de um switch, um hub não tem memória para armazenar quadros de dados.
- É importante entender que o mecanismo CSMA/CD não é implementado _dentro_ do hub. Em vez disso, a detecção e o tratamento de colisões ocorrem nos **adaptadores de rede** de cada dispositivo final conectado ao hub. 
- **Domínio de colisão**: Um "domínio de colisão" é uma área da rede onde as colisões de dados podem ocorrer. Como um hub simplesmente retransmite tudo para todos, todos os dispositivos conectados a um hub fazem parte de um **único e grande domínio de colisão**.
![[Pasted image 20250702154313.png]]