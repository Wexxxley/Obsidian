
---

 Ethernet é a tecnologia mais utilizada para construir redes locais LAN com fio.
- Simples e barata.
- Velocidade crescente, o padroa hoje é 10Gbps.
- Sem conexão, os dispositvos não precisam primeiro se conectar.


### **Processo de Transmissão com CSMA/CD:**
A Ethernet, em suas configurações mais antigas (como as baseadas em barramento ou hubs), utiliza um protocolo de acesso ao meio chamado **CSMA/CD

1. **Preparação para Transmissão:** O adaptador de rede recebe um pacote de dados (chamado "datagrama" na camada de rede) da camada superior e o encapsula, criando um **quadro** (frame) Ethernet.
    
2. **Sensoriamento do Canal e Início da Transmissão:**
    
    - O adaptador, então, verifica se o canal de comunicação está livre (**carrier sense**).
        
    - **Se o canal estiver livre**, o adaptador começa a transmitir o quadro imediatamente.
        
    - **Se o canal estiver ocupado**, o adaptador espera até que ele fique livre para iniciar a transmissão.
        
3. **Transmissão Bem-Sucedida:**
    
    - Se o adaptador conseguir transmitir o quadro inteiro (todos os seus bits) sem detectar nenhuma outra transmissão simultânea (ou seja, sem colisão), sua missão com aquele quadro está cumprida. O quadro foi enviado com sucesso para o meio.
        
4. **Detecção e Abortagem de Colisão:**
    
    - **Se o adaptador detectar outra transmissão (uma colisão) enquanto ele mesmo está transmitindo**, ele interrompe (aborta) imediatamente a transmissão do quadro atual.
        
    - Para garantir que todos os outros dispositivos na rede também percebam que uma colisão ocorreu (e assim não interpretem os sinais de colisão como dados válidos), o adaptador envia um sinal de congestionamento (também conhecido como "jam signal") para o canal.
        
5. **Mecanismo de "Exponential Backoff" (Espera Exponencial):**
    
    - Após abortar a transmissão devido a uma colisão, o adaptador não tenta retransmitir imediatamente. Para evitar que a mesma colisão ocorra repetidamente e para distribuir as tentativas de retransmissão no tempo, ele entra em um processo chamado **exponential backoff**.
        
    - Neste processo, o adaptador calcula um tempo de espera aleatório antes de tentar retransmitir. Esse tempo de espera aumenta exponencialmente com o número de colisões consecutivas:
        
        - Após a m-ésima colisão consecutiva, o adaptador escolhe um valor aleatório K dentro de um intervalo de {0,1,2,...,2m−1}.
            
        - O adaptador, então, espera por um período de K×512 tempos de bit (um "tempo de bit" é o tempo necessário para transmitir um único bit na velocidade da rede).
            
    - Após o período de espera, o adaptador retorna ao Passo 2, ou seja, ele volta a sensorear o canal para verificar se está livre e tenta transmitir novamente.
        

**Limitações e Evolução:**

O CSMA/CD é um protocolo eficiente para redes com carga de tráfego baixa a moderada. No entanto, em redes com alto tráfego ou muitos dispositivos, as colisões podem se tornar frequentes, diminuindo drasticamente a eficiência da rede.

Com o advento dos **switches Ethernet**, que operam em modo full-duplex (onde os dispositivos podem transmitir e receber simultaneamente sem colisões, pois cada porta de switch é um domínio de colisão separado), o CSMA/CD se tornou menos relevante nas redes modernas. Contudo, ele foi fundamental para o sucesso e a popularização inicial da tecnologia Ethernet.