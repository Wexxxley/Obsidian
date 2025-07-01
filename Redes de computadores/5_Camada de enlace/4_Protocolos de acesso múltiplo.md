
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

### **CSMA/CD (Protocolo de acesso aleatório -  Detecção de Colisão)**

O CSMA/CD é uma versão aprimorada do CSMA que, além de "ouvir antes de transmitir", também "ouve _enquanto_ transmite" para detectar colisões.

- **Colisões detectadas num tempo mais curto.** A principal vantagem do é que ele permite que os dispositivos detectem uma colisão logo que ela ocorre, e não apenas depois que todo o pacote já foi transmitido.
- Assim que uma colisão é detectada, os dispositivos envolvidos param imediatamente de transmitir o restante do pacote.

- **Detecção de colisão:**
 Em redes com fio como a Ethernet, detectar colisões é relativamente simples. O dispositivo monitora o nível de tensão no cabo. Se ele está transmitindo um sinal e detecta um nível de tensão maior ou um sinal diferente do que esperava, sabe que outra transmissão está ocorrendo simultaneamente, indicando uma colisão.
