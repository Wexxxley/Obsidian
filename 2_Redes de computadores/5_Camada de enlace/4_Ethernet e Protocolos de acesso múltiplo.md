
#Concluded 

--- 
### **Ethernet**
Ethernet é a tecnologia mais utilizada para construir redes locais LAN com fio.

- Simples e barata.
- Velocidade crescente, o padrão hoje é 10Gbps.
- **Sem conexão**, os dispositvos não precisam se conectar primeiro para iniciar uma transimissão.
- Se dois ou mais dispositivos tentarem transmitir ao mesmo tempo no canal compartilhado, seus sinais se misturarão e causarão interferência, ai que entra os protocolos de acesso.

- **Protocolo de múltiplo acesso:**
    - **Algoritmo distribuído:**  Algoritmo que todos os dispositivos da rede seguem para decidir quem pode transmitir e quando. 
    - **Comunicação sobre o compartilhamento do canal:** Para que os dispositivos coordenem quem transmite, eles precisam se comunicar. A ironia e o desafio é que essa "conversa" sobre quem vai usar o canal também precisa usar o _próprio canal_.
### **CSMA (Protocolo de acesso aleatório)**
Antes de um dispositivo enviar um quadro, ele "escuta" o canal para ver se ele está livre.
- **Se o canal parece vazio:** Ele assume que o caminho está livre e envia seus dados.
- **Se o canal está ocupado:** Ele espera por um período de tempo antes de tentar novamente.

Colisões ainda podem acontecer. Quando uma colisão acontece, os dados são corrompidos e o tempo gasto para enviar aquele pacote é perdido, pois ele precisará ser retransmitido.

### **CSMA/CD (Protocolo de acesso aleatório - Detecção de Colisão)**

1. **Início da Transmissão:**
    - O adaptador verifica se o canal de comunicação está livre. **Se o canal estiver livre**, o adaptador começa a transmitir o quadro imediatamente.
    - **Se o canal estiver ocupado**, o adaptador espera até que ele fique livre.
2. **Detecção e Abortagem de Colisão:**
    - Se acontecer colisão, ele interrompe imediatamente a transmissão do quadro atual e para garantir que todos os outros dispositivos na rede também percebam que uma colisão ocorreu, o adaptador envia um sinal de congestionamento.
3. **Espera Exponencial:**
    - Após a colisão, para evitar que a mesma colisão ocorra repetidamente ele entra em um processo chamado **exponential backoff**.
    - O adaptador calcula um tempo de espera antes de tentar retransmitir. Esse tempo de espera aumenta exponencialmente com o número de colisões consecutivas.
    - Após o período de espera, o adpatador volta a sensorear o canal.

