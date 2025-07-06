
---
#### **DropTail (FIFO)**
- É o tipo clássico de fila, configurado por padrão nos roteadores. 
- Quando cheia pacotes novos são descartados.
- A memória que deve ser alocada para a fila depende da capacidade(bps) e do atraso de propagação do enlace: ==M = Capacidde x Atraso de propagaçaõ== 
- Em enlace de 1 Gbps com atraso de propação de 20 ms deve ter uma fila com tamanho de 1 Gbps x 0,02 s = 20 Mb = 2,5 MB
- Memórias muito grandes podem causar atrasos, e muito pequanas ocorre muita perda de pacotes.
---
#### **Round-Robin (RR)**
- Em vez de uma única fila FIFO, os pacotes são separados em **múltiplas filas**, geralmente baseadas em alguma classificação (ex: tipo de serviço).
- O agendador visita cada fila de forma sequencial, enviando um pacote de cada fila antes de passar para a próxima. Se uma fila está vazia, ele pula para a próxima.

![Pasted image 20250606120427](../../attachments/Pasted%20image%2020250606120427.png)
- Não leva em conta a prioridade que um determinando paocte pode ter.

---
#### **Weighted Round-Robin**
- É uma evolução do Round-Robin. Ele também separa os pacotes em múltiplas filas, mas adiciona um **peso** a cada classe de tráfego.
- Por exemplo, se a Fila A tem peso 2 e a Fila B tem peso 1, a Fila A receberá terá o dobro de pacotes que a Fila B por ciclo do agendador.
- Permite que o administrador de rede priorize certas classes de tráfego. Mas nessecita de alterações constantes nos pesos

![Pasted image 20250606121409](../../attachments/Pasted%20image%2020250606121409.png)

---
#### **Stochastic Fair Queuing**
- Tenta diversificar os descartes nas conexões de forma proporcional ao número de pacotes da conexão, evitando o descarte de vários pacotes de uma mesma conexão e poucos pacotes de outra.

---
#### **Random Early Detection (RED)**
- **Comportamento:**
    - Monitora o **tamanho médio da fila**.
    - Quando a fila está abaixo de um limite mínimo, nenhum pacote é descartado.
    - Quando a fila está entre um limite mínimo e um limite máximo, o RED começa a **descartar pacotes aleatoriamente com base em uma porcentagem**.
    - Quando a fila atinge o limite máximo, ela usa um percentual mais brusco de descarte.
- **Vantagens:**
    - **Prevenção de Congestionamento:** Envia sinais de congestionamento para as sessões TCP _antes_ que a fila transborde, permitindo que elas reajam mais cedo.
    - **Quebra a Sincronização Global do TCP:** Ao descartar pacotes aleatoriamente e em momentos ligeiramente diferentes para diferentes fluxos, ele impede que todas as sessões TCP desacelerem simultaneamente.

---
#### **Hierárquica**
- Este não é um algoritmo de fila único, mas uma **arquitetura ou estrutura de enfileiramento** que combina diferentes tipos de filas para oferecer um controle de QoS muito granular e flexível.