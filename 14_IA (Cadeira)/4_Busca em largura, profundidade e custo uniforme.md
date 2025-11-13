
#Concluded 

---
![](../attachments/Pasted%20image%2020251031091210.png)

---
### **1. Busca em Largura (BFS - Breadth-First Search)**

A Busca em Largura é um algoritmo que explora as arestas de um grafo $G(V,A)$ para descobrir todos os vértices alcançáveis a partir de um vértice de origem $s \in V$.

A sua propriedade fundamental é que ela <mark style="background: #ADCCFFA6;">descobre todos os vértices a uma distância k de s antes de descobrir quaisquer vértices a uma distância k+1.</mark>

Para isso, a BFS utiliza uma estrutura de dados do tipo **Fila (Queue)**.

![](../attachments/Pasted%20image%2020251113194337.png)

---
### **2. Busca em Profundidade (DFS - Depth-First Search)**

A Busca em Profundidade é um algoritm que explora o mais fundo possível ao longo de cada ramo antes de retroceder.

A estratégia da DFS, ao contrário da BFS, <mark style="background: #ADCCFFA6;">é sempre expandir o último vértice descoberto na fronteira.</mark> Assim que um vértice $u$ é descoberto, a DFS explora iterativamente a partir de $u$, e só retorna para explorar outras arestas de $u$ quando toda a exploração descendente de $u$ estiver completa.

Para isso, a DFS utiliza uma estrutura de dados do tipo **Pilha (Stack)**

![](../attachments/Pasted%20image%2020251113194400.png)

---
### **3. Busca de Custo Uniforme (UCS - Uniform Cost Search)**

A Busca de Custo Uniforme é um algoritmo que explora o grafo $G(V,A)$ para encontrar o caminho de **menor custo total** de um vértice de origem $s$ até um vértice de destino.

A sua propriedade fundamental é que ela sempre expande o nó $n$ na fronteira que tem o **menor custo de caminho total** desde a origem $s$. Por causa disso, a UCS garante encontrar o caminho de menor custo para o destino.

Para isso, a UCS utiliza uma estrutura de dados do tipo **Fila de Prioridade (Priority Queue)**.

![](../attachments/Pasted%20image%2020251113194608.png)