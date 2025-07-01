
---
- **interferência:** Se dois ou mais dispositivos tentarem transmitir ao mesmo tempo nesse canal compartilhado, seus sinais se misturarão e causarão interferência.

- **Protocolo de múltiplo acesso:**
    - **Algoritmo distribuído:**  Um protocolo de acesso múltiplo é um algoritmo que todos os dispositivos da rede seguem para decidir quem pode transmitir e quando. É "distribuído" porque cada dispositivo toma suas próprias decisões.
    - **Comunicação sobre o compartilhamento do canal:** Para que os dispositivos coordenem quem transmite, eles precisam se comunicar. A ironia e o desafio é que essa "conversa" sobre quem vai usar o canal também precisa usar o _próprio canal_.

### **CSMA (Protocolo de acesso aleatório)**

Antes de um dispositivo enviar um quadro, ele "escuta" o canal para ver se ele está livre.
    - **Se o canal parece vazio:** Se o dispositivo não detecta outra transmissão, ele assume que o caminho está livre e envia seus dados.
    - **Se o canal está ocupado, adia a transmissão.** Se o dispositivo detecta que outro está transmitindo, ele espera por um período de tempo antes de tentar novamente.

Colisões ainda podem acontecer. Quando uma colisão acontece, os dados são corrompidos e o tempo gasto para enviar aquele pacote é perdido, pois ele precisará ser retransmitido.

### **CSMA/CD**

Este slide aprofunda o CSMA, introduzindo o "CD" (Collision Detection - Detecção de Colisão), que é uma melhoria do CSMA.

- **CSMA/CD (collision detection): detecção de portadora.** O CSMA/CD é uma versão aprimorada do CSMA que, além de "ouvir antes de transmitir", também "ouve _enquanto_ transmite" para detectar colisões.
    
- **Colisões detectadas num tempo mais curto.** A principal vantagem do CSMA/CD é que ele permite que os dispositivos detectem uma colisão _rapidamente_, logo que ela ocorre, e não apenas depois que todo o pacote já foi transmitido (e possivelmente perdido).
    
- **Transmissões com colisões são interrompidas, reduzindo o desperdício do canal.** Assim que uma colisão é detectada, os dispositivos envolvidos param imediatamente de transmitir o restante do pacote. Isso economiza tempo e largura de banda do canal, pois eles não continuam a enviar dados que já estão corrompidos. Eles então esperam um tempo aleatório e tentam retransmitir.
    
- **Detecção de colisão:**
    
    - **Fácil em LANs cabeadas: medição da intensidade do sinal, comparação dos sinais transmitidos e recebidos.** Em redes com fio como a Ethernet, detectar colisões é relativamente simples. O dispositivo monitora o nível de tensão no cabo. Se ele está transmitindo um sinal e detecta um nível de tensão maior ou um sinal diferente do que esperava, sabe que outra transmissão está ocorrendo simultaneamente, indicando uma colisão.
        
    - **Analogia humana: o "bom de papo" educado.** Essa analogia complementa a anterior do CSMA. Além de "não interromper os outros" (CSMA), o "bom de papo" educado (CSMA/CD) também "percebe se foi interrompido ou se falou ao mesmo tempo que outra pessoa" e para de falar, pedindo desculpas ou esperando a vez.