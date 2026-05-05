
---

Dado um grafo G = (V, E) e um vértice s, a busca em largura explora as arestas de G para “descobrir” cada vértice que pode ser alcançado a partir de s. O algoritmo calcula a distância (menor número de arestas) de s até cada vértice que pode ser alcançado.  Esse nome  foi dado ao algoritmo porque ele descobre os vértices em camadas. Primeiro os que estão à distância 1, depois distância 2 e por aí vai.

O algoritmo  Produz uma “**árvore de busca em largura**” com raiz s que contém todos os vértices que podem ser alcançados.  Para qualquer vértice v que pode ser alcançado de s, o caminho na árvore gerada corresponde a um “caminho mínimo”

Para controlar o progresso, a busca em largura pinta cada vértice de branco, cinza ou preto. No início, todos os vértices são brancos. Um vértice é descoberto na primeira vez em que é encontrado, nesse momento ele se torna cinza. Quando é finalizado um vértice, ou seja, descubro todos seus filhos, ele é pintado de preto.

  O procedimento de busca em largura (BFS) mostrado a seguir supõe que o grafo de entrada G = (V, E) é representado com a utilização de listas de adjacências.
  
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfqDGmzz0nt1xz_juqIDmHZucw7gb4z6S66ADCwCg-o_QLVVcZf03VHj08CusLQmS57ta_W51lde2nHItSXw9EvqkFVUoP1JxBFDG_72wbmDlmppOpsc9k3JM_OZRijYfnY158bXw?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Pseudocódigo do algoritmo.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfb1GlX0vX304ZMBM-SIBpdfnGC-2uIucY5lV6tYxfUh-7khz2mgeueGFjakSheRlbNyNebWYPEOrwjP2Qqn0ZNN2lNEAohZkUbtPRPHAHsnguijpR2wmmzEH9JvoKV9PeckzF2Bg?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Execução do algoritmo passo a passo.

  
