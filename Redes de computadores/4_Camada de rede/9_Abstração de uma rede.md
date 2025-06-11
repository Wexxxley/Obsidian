
---
[[1_Introdução a grafos|1_Introdução a grafos]]

Redes são abstraidas através de um grafo não direcionado com pesos.
![[Pasted image 20250531092212.png]]

---
### **1. Algoritmos de Roteamento Global vs. Descentralizado**

- **Algoritmo de Roteamento Global 
    - O reteador possui uma visão **global** de toda a topologia da rede, incluindo os custos de todos os links.

- **Algoritmo de Roteamento Descentralizado:**
    - Cada nó (roteador) começa sabendo apenas os custos dos links que estão **dos seus vizinhos**. 
    - O cálculo do caminho de menor custo é feito de forma **iterativa e distribuída**. Cada nó troca informações com seus vizinhos. Com base nas informações recebidas e nos custos de seus próprios links, cada nó gradualmente calcula as rotas de menor custo para todos os destinos na rede.
### **2. Algoritmos de Roteamento Estáticos vs. Dinâmicos**

- **Algoritmos de Roteamento Estáticos:**
    - As rotas mudam muito **lentamente** ao longo do tempo.
    - Geralmente, as mudanças são resultado de **intervenção humana** (um administrador de rede configurando manualmente as tabelas de roteamento do roteador).
    - Comuns em redes pequenas.

- **Algoritmos de Roteamento Dinâmicos:**
    - As rotas se **adaptam automaticamente** e mudam rapidamente em resposta a alterações na rede.
    - Mudanças ocorrem quando há congestionamento ou na mudanças **topologia da rede** (links caem, novos links surgem, roteadores falham).
    - Podem rodar periodicamente (a cada X segundos) ou ser acionados por eventos (uma mudança detectada).

---
### **3. Algoritmo Link State (LS)**
Computa caminhos de menor custo de um nó (fonte) para todos os outros nós:
- Fornece uma tabela de roteamento para aquele nó.
- Algoritmo global e estáticos.

[[3_Caminho mínimo de fonte única (Dijkstra)]]

### **4. Algoritmo Vetor de distância (VD)**

Todo nó mantém uma **tabela de vetor de distância**, que contém suas estimativas de distância para todos os destinos na rede 

Esse algorítmo é assíncrono e iterativo.
- Um nó só envia sua **tabela de vetor de distância** para seus vizinhos se houver alguma alteração.
- Se o vizinho de um nó recebe uma atualização que o faz recalcular suas próprias rotas de forma a mudar seu DV, esse vizinho, por sua vez, notificará seus vizinhos, e assim por diante. 

- Quando o nó x recebe nova estimativa D(v) do vizinho, ele atualiza seu próprio D(v) usando a equação Bellman-Ford: dist(v)=min(dist(v),dist(u)+w) para cada nó v E N

