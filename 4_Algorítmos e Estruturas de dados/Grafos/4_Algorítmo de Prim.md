


---
Primeiro é importante conhecer o conceito de corte de um grafo: Dado um grafo $G=(V,E)$, um corte é uma partição do conjunto de vértices V em dois subconjuntos S e V - S.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfML2G_rZQku82DAyHZzDswGakwGvX_VkexwURkns6k0Qm38yAcE_ptGlz0B7Wy3jmUABE4kTxAQ1iJ7Kv6HyAHd7WY8PI8KLz2coSfdYZ9slb-0kBrZz2Xgem8gHJbIOe_Uo_94Q?key=VJjD-GQ4BeMLFSL3weHQfxOz)

No algoritmo de prim, esse conceito de corte é usado para decidir quais arestas podem ser adicionadas à árvore geradora mínima. 

**Pseudocódigo do algoritmo de Prim.** 
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfJCCh5dFoRLi0Lfvl1G1anKTXWjM7Q_sGjTGIn724_TkhUf7eQReH7WzR7W_Ikz7gvsnsiVeoN2eUdmDGolv9M4Ao4pw93dhZZE7Q_gwW_TxaD_n53DpuxRuBE-v80mP5oF7ZxHA?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Cada vértice do grafo é inicializado: 
- u.key  = infinity: representa o custo para incluir o vértice na árvore.
- u.pai = null: indica que o vértice ainda não foi conectado à árvore.
  
 Depois é definido r.key = 0, pois ele é o vértice inicial. Então, é criado Q com todos os vértices. Q é uma fila de prioridade, ou seja, os elementos com as menores chaves são retirados primeiro.

  Temos um loop nas linhas 6-11. Enquanto a fila não for vazia é retirado o vértice u com menor chave. Para cada vétice u retirado da fila, é feito um for com cada vértice v adjacente a u. Então, cada vértice adjacente a u tem seu pai e peso atualizado. Após verificar todos os vértices adjacentes a u o for acaba e o vértice com menor peso da fila é retirado. O processo se repete até a fila estar vazia.

  
**Complexidade**: Ambos Kruskal e Prim são da ordem O(m log n).
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcSx2XwO8LWqzqZnnxM6PiGIYrN9AslE7tf0w26OsnYcSDl6RiLaUkDNxY26aA9h_ELymVHql3FvF4_iAqxlWvkIwomSWAfGcgUJOWEfsF4y7v0pOJrHZ_-FkWh0GbUFmfUaWNlxQ?key=VJjD-GQ4BeMLFSL3weHQfxOz)




  
  