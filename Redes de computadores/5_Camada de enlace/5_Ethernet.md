
---

### **Processo de Transmissão com CSMA/CD:**
A Ethernet, em suas configurações mais antigas (como as baseadas em barramento ou hubs), utiliza um protocolo de acesso ao meio chamado **CSMA/CD

1. **Preparação para Transmissão:** O adaptador de rede recebe um pacote de dados e o encapsula, criando um **quadro** (Ethernet.
2. **Início da Transmissão:**
    - O adaptador verifica se o canal de comunicação está livre. **Se o canal estiver livre**, o adaptador começa a transmitir o quadro imediatamente.
    - **Se o canal estiver ocupado**, o adaptador espera até que ele fique livre.
3. **Detecção e Abortagem de Colisão:**
    - Se acontecer colisão, ele interrompe imediatamente a transmissão do quadro atual e para garantir que todos os outros dispositivos na rede também percebam que uma colisão ocorreu, o adaptador envia um sinal de congestionamento.
4. **Espera Exponencial:**
    - Após a colisão, para evitar que a mesma colisão ocorra repetidamente ele entra em um processo chamado **exponential backoff**.
    - Neste processo, o adaptador calcula um tempo de espera aleatório antes de tentar retransmitir. Esse tempo de espera aumenta exponencialmente com o número de colisões consecutivas:
    - Após o período de espera, o adpatador volta a sensorear o canal.

Com o advento dos **switches Ethernet**, que operam em modo full-duplex, o CSMA/CD se tornou menos relevante nas redes modernas. 