

---
O problema da sincronização global do TCP ocorre quando múltiplas sessões TCP, que atravessam um mesmo roteador congestionado, perdem pacotes **ao mesmo tempo** e, consequentemente, **reduzem suas taxas de envio simultaneamente**. Quando voltam a normalizar aumetam ao a taxa de tranferencia ao mesmo tempo causando um ciclo de subir a taxa de tranferencia e descer a taxa de tranferencia

Aqui está a sequência de eventos que leva a isso:

1. **Fila cheia:** Várias sessões TCP estão enviando dados através de um roteador. A taxa de chegada de pacotes ao buffer de saída do roteador excede a capacidade de saída do link. A fila começa a crescer rapidamente.
2. **Descarte em Massa (Tail Drop):** A fila atinge sua capacidade máxima. O roteador começa a descartar todos os pacotes que chegam subsequentes. Crucialmente, como o descarte ocorre no final da fila, **muitas sessões TCP diferentes, que estavam usando o link, perdem pacotes quase ao mesmo tempo**.
3. **Detecção de Perda e Reação Sincronizada:**
    - Cada uma das sessões TCP que perdeu pacotes detecta essa perda (via timeout ou ACKs duplicados).
    - Como reação ao congestionamento, **todas essas sessões TCP simultaneamente entram em suas fases de controle de congestionamento**, reduzindo suas janelas de congestionamento e, portanto, suas taxas de envio.
4. **Subutilização da Largura de Banda:** Com muitas sessasões desacelerando ao mesmo tempo, o link que estava congestionado de repente fica **subutilizado**. A fila do roteador esvazia.
5. **Aumento Sincronizado (Slow Start/Congestion Avoidance):** Após a redução, todas as sessões TCP iniciam simultaneamente o processo de aumento lento de suas taxas de envio para sondar a rede novamente (slow start e congestion avoidance).
6. **Novo Congestionamento:** Como todas as sessões estão aumentando suas taxas de envio ao mesmo tempo, elas rapidamente **voltam a congestionar o mesmo roteador e enchem sua fila novamente**.
7. **Ciclo Vicioso:** O roteador volta a descartar pacotes em massa, e o ciclo se repete.

**Resultado:** Em vez de uma utilização suave e eficiente da largura de banda, a rede experimenta um comportamento de "montanha-russa": períodos de **congestionamento severo e descarte em massa**, seguidos por períodos de **subutilização da largura de banda**, seguidos por mais congestionamento. Isso leva a:

- **Baixa Taxa de Transferência (Throughput):** A largura de banda total do link não é utilizada de forma eficiente.
- **Alta Latência e Variação de Latência (Jitter):** As filas crescem e diminuem drasticamente, causando atrasos variáveis.
- **Aumento de Perda de Pacotes:** Os descartes massivos continuam ocorrendo.

### Solução: AQM (Active Queue Management)

A solução primária para a sincronização global do TCP é o uso de algoritmos de **Gerenciamento Ativo de Filas (Active Queue Management - AQM)** nos roteadores.

Em vez de esperar que a fila esteja completamente cheia para começar a descartar pacotes (tail drop), os algoritmos AQM começam a descartar pacotes _preventivamente_ antes que a fila transborde. Mais importante, eles fazem isso de forma **aleatória** e **probabilística**.

O algoritmo AQM mais conhecido é o **RED (Random Early Detection)**:

- **Detecção Precoce (Early Detection):** O RED monitora o tamanho médio da fila. Quando a fila começa a crescer, mas ainda está abaixo de um certo limite, ele começa a descartar pacotes com uma probabilidade _baixa_.
- **Descarte Aleatório (Random Discard):** A probabilidade de descarte aumenta linearmente à medida que a fila cresce, até atingir um segundo limite, quando todos os pacotes são descartados (como no tail drop).
- **Prevenção da Sincronização:** Ao descartar pacotes de forma aleatória e gradual, o RED faz com que as diferentes sessões TCP recebam o sinal de congestionamento em **momentos ligeiramente diferentes**. Isso impede que todas as sessões reduzam suas taxas de envio ao mesmo tempo, quebrando o ciclo de sincronização global. As sessões TCP se adaptam ao congestionamento de forma mais _assíncrona_, resultando em uma utilização de largura de banda mais suave e consistente.

Em resumo, a sincronização global do TCP é um problema de eficiência causado pela reação coordenada de múltiplas sessões TCP ao congestionamento, levando a um ciclo de superutilização e subutilização da rede. Os algoritmos AQM, como o RED, são a principal contramedida, introduzindo aleatoriedade nos descartes para quebrar essa sincronização e promover uma utilização mais estável e eficiente da largura de banda disponível.