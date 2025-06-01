
---
[[1_Introdução a grafos|1_Introdução a grafos]]

Redes são abstraidas através de um grafo não direcionado com pesos.
![[Pasted image 20250531092212.png]]

---
### **1. Algoritmos de Roteamento Global vs. Descentralizado**
Esta classificação se refere à **forma como os roteadores obtêm e utilizam as informações sobre a rede** para calcular as rotas.

- **Algoritmo de Roteamento Global 
    - **Conhecimento:** Possui uma visão **completa e global** de toda a topologia da rede, incluindo os custos de todos os links.
    - **Como funciona:** Antes de iniciar o cálculo das rotas, o algoritmo precisa coletar todas essas informações. Isso pode ser feito de forma centralizada (um único local calcula tudo) ou replicada (várias cópias do algoritmo, cada uma com o conhecimento global, calculam as rotas).

- **Algoritmo de Roteamento Descentralizado:**
    - **Conhecimento:** Cada nó (roteador) começa sabendo apenas os custos dos links que estão **diretamente conectados a ele (seus vizinhos)**. 
    - **Como funciona:** O cálculo do caminho de menor custo é feito de forma **iterativa e distribuída**. Cada nó troca informações com seus vizinhos. Com base nas informações recebidas e nos custos de seus próprios links, cada nó gradualmente calcula (ou atualiza) as rotas de menor custo para todos os destinos na rede.

### **2. Algoritmos de Roteamento Estáticos vs. Dinâmicos**
Esta classificação se refere à **frequência e forma como as rotas são alteradas**.
- **Algoritmos de Roteamento Estáticos:**
    - **Mudança de Rotas:** As rotas mudam muito **lentamente** ao longo do tempo.
    - **Causa da Mudança:** Geralmente, as mudanças são resultado de **intervenção humana** (um administrador de rede configurando manualmente as tabelas de roteamento do roteador).
    - **Uso:** Comuns em redes pequenas.

- **Algoritmos de Roteamento Dinâmicos:**
    - **Mudança de Rotas:** As rotas se **adaptam automaticamente** e mudam rapidamente em resposta a alterações na rede.
    - **Causa da Mudança:** Mudanças ocorrem quando há variações há congestionamento ou na **topologia da rede** (links caem, novos links surgem, roteadores falham).
    - **Como funcionam:** Podem rodar periodicamente (a cada X segundos) ou ser acionados por eventos (uma mudança detectada).
    - **Vantagens:** Mais sensíveis e adaptáveis às condições reais da rede.

---
### **3. Algoritmo Link State (LS)**
Computa caminhos de menor custo de um nó (fonte) para todos os outros nós:
- Fornece uma tabela de roteamento para aquele nó.
- Algoritmo global e estáticos.

[[3_Caminho mínimo de fonte única (Dijkstra)]]

### **4. Algoritmo Vetor de distância (VD)**


**Iterativo e assincrono**
- **Iterativo:** O algoritmo funciona em iterações". Cada nó da rede não calcula tudo de uma vez; ele refina suas estimativas de distância ao longo do tempo, em várias rodadas.
- **Assíncrono:** As iterações não acontecem de forma sincronizada em todos os nós da rede. Cada nó realiza uma iteração local quando duas condições são satisfeitas:
    - **Mudança no custo do enlace local:** Se custo de usar uma conexão direta para um vizinho mudar o nó precisa recalcular suas rotas.
    - **Mensagem de atualização DV do vizinho:** Se um nó vizinho envia sua própria tabela de distâncias atualizada, o nó receptor precisa processar essa informação para tentar encontrar caminhos mais curtos.

### 2. Distribuído

- **Cada nó notifica os vizinhos apenas quando seu DV mudar:** Isso é uma otimização importante. Um nó só envia sua tabela de vetor de distância (que contém suas estimativas de distância para todos os destinos na rede) para seus vizinhos se houver alguma alteração significativa em suas próprias rotas. Isso evita o tráfego de rede desnecessário.
- **Os vizinhos então notificam seus vizinhos, se necessário:** Esta é a parte "iterativa" e "distribuída". Uma mudança em um nó pode cascatear por toda a rede. Se o vizinho de um nó recebe uma atualização que o faz recalcular suas próprias rotas de forma a mudar seu DV, esse vizinho, por sua vez, notificará seus vizinhos, e assim por diante. É um processo de "fofoca" controlada sobre as melhores rotas.

### 3. Fluxo de Operação para Cada Nó (o Fluxograma à Direita)

Para cada nó na rede, o processo é o seguinte:

1. **espera:** O nó fica inativo, esperando por um evento que exija uma ação. Esse evento pode ser:
    
    - Uma mudança no custo de um de seus enlaces diretos (locais).
    - O recebimento de uma mensagem de atualização de Vetor de Distância (DV) de um de seus vizinhos.
2. **recalcula estimativas:** Uma vez que um evento ocorre, o nó recalcula suas estimativas de distância para todos os destinos na rede. Ele faz isso usando a famosa **Equação de Bellman-Ford (ou Ford-Fulkerson)**:
    
    - Para cada destino `D`, o nó `N` calcula a distância para `D` através de cada um de seus vizinhos `V`.
    - A distância para `D` via `V` é o custo do enlace de `N` para `V` mais a distância de `V` para `D` (informada pelo vizinho `V` em sua última mensagem DV).
    - O nó `N` então escolhe o caminho que resulta na menor distância total para `D` e atualiza sua própria tabela de roteamento.
3. **se o DV para qualquer destino mudou, notifica os vizinhos:** Após recalcular suas estimativas, o nó compara seu novo Vetor de Distância (DV) com o DV anterior. Se houver qualquer mudança (ou seja, se ele encontrou um caminho mais curto para um destino, ou se um caminho anterior se tornou mais longo/inacessível), ele empacota seu novo DV e o envia para todos os seus vizinhos diretos. Isso permite que os vizinhos, por sua vez, recalculem suas próprias rotas, dando início a uma nova iteração distribuída.
    

### Em Resumo

O Algoritmo de Vetor de Distância é uma abordagem descentralizada para roteamento, onde cada roteador mantém uma tabela (o "vetor de distância") das distâncias conhecidas para todos os outros roteadores na rede e o próximo salto para alcançá-los. Ele compartilha essas informações com seus vizinhos e usa as informações recebidas para atualizar suas próprias tabelas. A comunicação ocorre de forma assíncrona, impulsionada por mudanças na rede ou por atualizações dos vizinhos, permitindo que a informação sobre as melhores rotas se propague por toda a rede de forma iterativa.