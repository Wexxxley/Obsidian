
---

### **Hub**
Um hub opera na **Camada 1 (Física)**. Um hub é basicamente um repetidor de sinais elétricos. Ele não "entende" os dados da mesma forma que um switch ou roteador.

- **Broadcast**: Quando um bit chega a uma das portas do hub, ele é imediatamente copiado e enviado para _todas_ as outras portas conectadas. Isso significa que todos os dispositivos conectados ao hub recebem cada bit de dados transmitido por qualquer outro dispositivo no mesmo hub.
- **Um hub não faz conversão de velocidade**.
- **Não possuem armazenagem de quadros.** Ao contrário de um switch, um hub não tem memória para armazenar quadros de dados.
- É importante entender que o mecanismo CSMA/CD não é implementado _dentro_ do hub. Em vez disso, a detecção e o tratamento de colisões ocorrem nos **adaptadores de rede** de cada dispositivo final conectado ao hub. 
- **Domínio de colisão**: Um "domínio de colisão" é uma área da rede onde as colisões de dados podem ocorrer. Como um hub simplesmente retransmite tudo para todos, todos os dispositivos conectados a um hub fazem parte de um **único e grande domínio de colisão**.
![[Pasted image 20250702154313.png]]


---
### **Switch**
Um switch é um **dispositivo de camada de enlace**. Diferente dos hubs, os switches são capazes de "entender" e processar os quadros Ethernet.

- **Armazena e encaminha quadros Ethernet:** Ao receber um quadro de dados, o switch o armazena temporariamente antes de tomar uma decisão de encaminhamento.
- **Unicast**: Um switch lê o **end MAC** de destino e encaminha o quadro apenas para a porta específica. Isso cria segmentos, onde cada porta se torna um domínio de colisão individual.
- **Transparente:** Isso significa que os computadores conectados à rede não "percebem" a presença do switch; eles simplesmente enviam seus dados, e o switch cuida do encaminhamento. Não há necessidade de configuração

[[3_MAC e ARP]]
**Tabela do Switch:**
A inteligência de um switch reside em sua capacidade de aprender as localizações dos dispositivos conectados a ele. Para isso, ele mantém uma **tabela**, a tabela MAC.

- **Como o Aprendizado Acontece:** Quando um switch recebe um quadro ele automaticamente aprende a localização do transmissor.
- Cada entrada tem um tempo de vida, que pode ser, por exemplo, 60 minutos. Se um dispositivo não transmitir por esse período, sua entrada é removida, mantendo a tabela atualizada e eficiente.

**Lógica de Encaminhamento:**
Quando um switch recebe um quadro Ethernet, ele segue uma lógica precisa para decidir como encaminhá-lo:

1. O switch primeiro verifica o **endereço MAC de destino** no cabeçalho do quadro. Ele usa esse endereço para pesquisar em sua tabela.
2. **Se a Entrada for Encontrada:**
    - O switch então encaminha o quadro _somente_ para essa interface específica.
    - Se o quadro chegou em uma interface e o endereço MAC de destino também está associado à _mesma_ interface, o switch simplesmente **descarta o quadro do buffer**. 
    - Se o destino está em uma interface diferente da de origem, ele reencaminha o quadro na interface indicada na tabela.
3. **Se Nenhuma Entrada for Encontrada para o Destino (Flood):**
    
    - **Inundação (Flood):** Se o switch **não encontrar o endereço MAC de destino** em sua tabela (porque é um dispositivo novo na rede ou a entrada expirou), ele não sabe onde enviar o quadro seletivamente. Nesse caso, ele entra em modo de **inundação (flood)**.
        
    - Isso significa que o switch **encaminha o quadro para todas as suas interfaces, exceto para a interface pela qual o quadro chegou**. Isso garante que o quadro alcance seu destino (que provavelmente responderá, permitindo que o switch aprenda sua localização para futuras comunicações) e é uma forma de "descoberta" de endereços MAC.
        

Em resumo, os switches revolucionaram as redes locais ao trazer inteligência para a Camada 2, eliminando a ineficiência dos hubs através do encaminhamento seletivo baseado em endereços MAC e da criação de múltiplos domínios de colisão, resultando em redes mais rápidas, eficientes e confiáveis.