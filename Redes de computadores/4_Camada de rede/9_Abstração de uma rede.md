
---
[[1_Introdução a grafos|1_Introdução a grafos]]

Redes são abstraidas através de um grafo não direcionado com pesos.
![[Pasted image 20250531092212.png]]

---
### **1. Algoritmos de Roteamento Global vs. Descentralizado**
Esta classificação se refere à **forma como os roteadores obtêm e utilizam as informações sobre a rede** para calcular as rotas.

- **Algoritmo de Roteamento Global **
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
### **3. Algoritmo de Dijsktra**


