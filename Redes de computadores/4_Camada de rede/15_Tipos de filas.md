
---
### **DropTail (FIFO)**
- É o tipo clássico de fila, configurado por padrão nos roteadores. 
- Quando cheia pacotes novos são descartados.
- A memória que deve ser alocada para a fila depende da capacidade(bps) e do atraso de propagação do enlace: ==M = Capacidde x Atraso de propagaçaõ== 
- Em enlace de 1 Gbps com atraso de propação de 20 ms deve ter uma fila com tamanho de 1 Gbps x 0,02 s = 20 Mb = 2,5 MB
- Memórias muito grandes podem causar atrasos, e muito pequanas ocorre muita perda de pacotes.
---
#### **Round-Robin (RR)**
- Em vez de uma única fila FIFO, os pacotes são separados em **múltiplas filas**, geralmente baseadas em alguma classificação (ex: tipo de serviço).
- O agendador visita cada fila de forma sequencial (round-robin), enviando um pacote (ou um número fixo de bytes) de cada fila antes de passar para a próxima. Se uma fila está vazia, ele pula para a próxima.
As conexões são divididas em classes e cada classe tem o mesmo tempo de processamento. Pode ser injusta com classes com maior volume de tráfego
![[Pasted image 20250606120427.png]]

 Weighted Round-Robin (WRR)
 Stochastic Fair Queuing (SFQ)
 Random Early Detection (RED)
 Hierárquica

#### 2. Round-Robin (RR)
-
- **Vantagens:** Proporciona um nível de justiça básico entre os fluxos ou classes de tráfego, garantindo que nenhum fluxo monopolize totalmente a largura de banda.
- **Desvantagens:** Não leva em conta a importância ou a necessidade de largura de banda de diferentes tipos de tráfego. Todos os fluxos recebem a mesma "fatia" de tempo de serviço.

#### 3. Weighted Round-Robin (WRR)

- **Explicação:** O WRR é uma evolução do Round-Robin. Ele também separa os pacotes em múltiplas filas, mas adiciona um **peso (weight)** a cada fila ou classe de tráfego.
- **Comportamento:** Em vez de dar a mesma fatia de tempo a cada fila, o WRR dá a cada fila uma fatia de largura de banda **proporcional ao seu peso**. Por exemplo, se a Fila A tem peso 2 e a Fila B tem peso 1, a Fila A receberá o dobro de largura de banda (ou terá o dobro de pacotes/bytes enviados) que a Fila B por ciclo do agendador.
- **Vantagens:** Permite que o administrador de rede priorize certas classes de tráfego, alocando-lhes uma maior proporção da largura de banda disponível. É uma forma de fornecer QoS (Quality of Service) básica.
- **Desvantagens:** Ainda não lida com o congestionamento de forma proativa (como o RED) e pode ter problemas de latência se a fila de alta prioridade estiver sempre cheia.

#### 4. Stochastic Fair Queuing (SFQ)

- **Explicação:** O SFQ é um algoritmo projetado para fornecer um tipo de **justiça (fairness)** entre os diferentes fluxos de tráfego, evitando que um único fluxo monopolize a fila. É considerado uma forma de Fair Queuing.
- **Comportamento:** Em vez de ter filas para classes pré-definidas, o SFQ tenta alocar um slot de fila separado para _cada fluxo individual_ (ou um pequeno grupo de fluxos) com base em um hashing dos cabeçalhos dos pacotes (endereços IP de origem/destino, portas, etc.). Como o número de fluxos pode ser muito grande, ele usa um número limitado de filas "virtuais" e um algoritmo de hashing "estocástico" (aleatório) para tentar distribuir os fluxos uniformemente nessas filas. O agendador então opera em Round-Robin entre essas filas.
- **Vantagens:**
    - Melhora a justiça entre os fluxos, mesmo em cenários de muitos fluxos.
    - Ajuda a prevenir o "domínio" de um único fluxo sobre outros.
    - Melhora o desempenho do TCP em ambientes congestionados, pois cada fluxo TCP percebe um buffer "menor" e mais isolado.
- **Desvantagens:** Pode ter um overhead de processamento maior do que as filas FIFO. A aleatoriedade do hashing pode, ocasionalmente, levar a colisões de fluxos na mesma fila, diminuindo a justiça.

#### 5. Random Early Detection (RED)

- **Explicação:** O RED não é um algoritmo de agendamento de filas como RR ou WRR. Em vez disso, é um algoritmo de **Gerenciamento Ativo de Filas (AQM)** que trabalha em conjunto com outras disciplinas de fila (como DropTail, embora seu uso seja mais eficaz com uma única fila lógica) para **prevenir o congestionamento** antes que ele se torne severo.
- **Comportamento:**
    - Monitora o **tamanho médio da fila**.
    - Quando a fila está abaixo de um limite mínimo (`min_th`), nenhum pacote é descartado.
    - Quando a fila está entre um limite mínimo (`min_th`) e um limite máximo (`max_th`), o RED começa a **descartar pacotes aleatoriamente com uma probabilidade crescente**. Quanto maior a fila média nesse intervalo, maior a probabilidade de descarte.
    - Quando a fila atinge o limite máximo (`max_th`), todos os pacotes novos são descartados (DropTail).
- **Vantagens:**
    - **Prevenção de Congestionamento:** Envia sinais de congestionamento (descartando alguns pacotes) para as sessões TCP _antes_ que a fila transborde, permitindo que elas reajam mais cedo.
    - **Quebra a Sincronização Global do TCP:** Ao descartar pacotes aleatoriamente e em momentos ligeiramente diferentes para diferentes fluxos, ele impede que todas as sessões TCP desacelerem simultaneamente.
    - **Evita Atrasos Excessivos:** Ajuda a manter os buffers das filas em um tamanho gerenciável, reduzindo o atraso de enfileiramento percebido pelos usuários.
- **Desvantagens:** A configuração dos limites e da probabilidade de descarte pode ser complexa e impactar o desempenho se não for feita corretamente. É mais eficaz com tráfego TCP.

#### 6. Hierárquica

- **Explicação:** Este não é um algoritmo de fila único, mas uma **arquitetura ou estrutura de enfileiramento** que combina diferentes tipos de filas para oferecer um controle de QoS muito granular e flexível.
- **Comportamento:** Em um sistema de filas hierárquico, você pode ter múltiplas "camadas" de filas e agendamento.
    - Por exemplo, no nível superior, você pode ter um agendador WRR que aloca largura de banda para classes de tráfego principais (Voz, Vídeo, Dados).
    - Dentro de cada uma dessas classes (nível inferior), você pode ter outro tipo de fila ou agendador (ex: SFQ ou outro WRR) para garantir justiça ou priorização dentro daquela classe.
    - Cada uma dessas sub-filas pode, por sua vez, ter um AQM (como RED) configurado.
- **Vantagens:** Permite um controle de QoS extremamente sofisticado e granular. Você pode, por exemplo, garantir uma largura de banda mínima para o tráfego de voz, dar preferência a ele sobre o vídeo, e depois distribuir a largura de banda restante de forma justa entre todos os fluxos de dados, tudo isso enquanto previne o congestionamento.
- **Desvantagens:** É o tipo mais complexo de configurar e exige um planejamento cuidadoso e recursos de hardware significativos no roteador.