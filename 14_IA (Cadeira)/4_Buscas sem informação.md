
#Concluded 

---
Esses algoritmos não possuem nenhuma informação sobre a "proximidade" do estado atual em relação ao estado objetivo. Eles conseguem apenas gerar sucessores e distinguir se um estado é o objetivo ou não.

---
### **1. Busca em Largura (BFS - Breadth-First Search)**

Expande a fronteira uniformemente em camadas. Primeiro visita todos os nós a uma distância $k$ da origem antes de visitar qualquer nó a distância $k+1$.

- Para isso, a BFS utiliza uma estrutura de dados do tipo **Fila (Queue)**.
- Ela é ótima se todos as arestas tiverem mesmo peso.
- Ela precisa manter toda a fronteira em memória.
![](../attachments/Pasted%20image%2020251204145544.png)

---
### **2. Busca em Profundidade (DFS - Depth-First Search)**

A Busca em Profundidade é um algoritm que explora o mais fundo possível ao longo de cada ramo antes de retroceder.

- Para isso, a DFS utiliza uma estrutura de dados do tipo **Pilha (Stack)**
- Seu resultado não é ótimo

![](../attachments/Pasted%20image%2020251204145647.png)

---
### **3. Busca de Custo Uniforme (UCS - Uniform Cost Search)**

A sua propriedade fundamental é que ela sempre expande o nó $n$ na fronteira que tem o **menor custo de caminho total** desde a origem $s$. A UCS garante encontrar o caminho de menor custo para o destino.

Para isso, a UCS utiliza uma estrutura de dados do tipo **Fila de Prioridade (Priority Queue)**.

![](../attachments/Pasted%20image%2020251204145628.png)

Mas para priorityQUeue funcionar, é preciso definir como comarar dois nós
![](../attachments/Pasted%20image%2020251204145013.png)

---  

**DEQUE**
- popleft(), pop()
- append()

**PRIORITYQUEUE**
- get()
- put()