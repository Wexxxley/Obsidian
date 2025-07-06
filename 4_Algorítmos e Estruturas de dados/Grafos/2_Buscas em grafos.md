
---
### **1. Busca em largura**

 Dado um grafo G = (V, E) e um vértice s, a busca em largura explora as arestas de G para “descobrir” cada vértice que pode ser alcançado a partir de s. O algoritmo calcula a distância (menor número de arestas) de s até cada vértice que pode ser alcançado.  Esse nome  foi dado ao algoritmo porque ele descobre os vértices em camadas. Primeiro os que estão à distância 1, depois distância 2 e por aí vai.

  

 O algoritmo  Produz uma “árvore de busca em largura” com raiz s que contém todos os vértices que podem ser alcançados.  Para qualquer vértice v que pode ser alcançado de s, o caminho na árvore gerada corresponde a um “caminho mínimo”

  

 Para controlar o progresso, a busca em largura pinta cada vértice de branco, cinza ou preto. No início, todos os vértices são brancos. Um vértice é descoberto na primeira vez em que é encontrado, nesse momento ele se torna cinza. Quando é finalizado um vértice, ou seja, descubro todos seus filhos, ele é pintado de preto.

  

 O procedimento de busca em largura (BFS) mostrado a seguir supõe que o grafo de entrada G = (V, E) é representado com a utilização de listas de adjacências.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfqDGmzz0nt1xz_juqIDmHZucw7gb4z6S66ADCwCg-o_QLVVcZf03VHj08CusLQmS57ta_W51lde2nHItSXw9EvqkFVUoP1JxBFDG_72wbmDlmppOpsc9k3JM_OZRijYfnY158bXw?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Pseudocódigo do algoritmo.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfb1GlX0vX304ZMBM-SIBpdfnGC-2uIucY5lV6tYxfUh-7khz2mgeueGFjakSheRlbNyNebWYPEOrwjP2Qqn0ZNN2lNEAohZkUbtPRPHAHsnguijpR2wmmzEH9JvoKV9PeckzF2Bg?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Execução do algoritmo passo a passo.

  

___________________________________________________________________________

### 1.3 Busca em profundidade

 A estratégia seguida pela busca em profundidade é, como seu nome implica, buscar o “mais fundo” no grafo, sempre que possível. A busca em profundidade explora arestas partindo do vértice v mais recentemente descoberto.  Depois que todas as arestas de v foram exploradas, a busca regressa para explorar as arestas que partem do pai de v. Esse processo continua até descobrirmos todos os vértices que podem ser visitados a partir do vértice fonte. Se restarem quaisquer vértices não descobertos, a busca em profundidade seleciona um deles como fonte e repete a busca partindo dessa fonte. 

 Como na busca em largura, a busca em profundidade pinta os vértices durante a busca para indicar o estado de cada um. A busca em profundidade também identifica cada vértice com um carimbo de tempo. Cada vértice v tem dois carimbos de tempo: o primeiro carimbo de tempo v.d registra quando v é descoberto pela primeira vez, e o segundo carimbo de tempo v.f registra quando a busca termina de examinar a lista de adjacências de v.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcODPgn3qwUJNNRN4mT5UJMK_O7sfWBXJ1mZ9pZA9g9DnH3Y_bsX-GRBi-5C6_QECIlOcF7ONranMhnb23x2O6R7Q87qcIKHhKCsJBhLVOz86cJ3sMhlu4SX-MwFcBnq9WEC4XZuA?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Pseudocódigo do algoritmo.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdqk2nxLkBto4Tcwmet4S8d9po5mloy48M4TfaLDtw06MYXYsEQu0vvJ9LQCqaPYmnEAxy7ERr7hl2pfF731aqMJAKh3M3CS59HbKB8tYJv4nTymEHyD03WvLhkcradEwyQcrD2xQ?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Passo a passo do algoritmo.

  

 O subgrafo dos predecessores de uma busca em profundidade forma uma floresta de busca em profundidade que abrange várias árvores de busca em profundidade. 

  Uma propriedade importante da busca em profundidade é que os tempos de descoberta e término têm estrutura parentizada. Se representarmos a descoberta do vértice u com um parêntese à esquerda “(u” e representarmos seu término por um parêntese à direita “u)”, então é gerado uma expressão bem formada, no sentido de que os parênteses estão adequadamente aninhados. Por exemplo, a busca em profundidade da figura a seguir contém a sua estrutura parentizada.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfdKMyfoxX9zZO4qsVLILs9DgOGcKuNmV75jDJw1yg5FK5_8aflFQmJUwbt0z3uVEeiIr4avryLPE7Mv1x48xxpfcyW4WcT-XcNa9yoakg3Jby3gVHuj86g4uxvRKjthXSEidQY?key=VJjD-GQ4BeMLFSL3weHQfxOz)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeoTuocFB5xg290CCuGO_RgEoiC28Rhl-ArK9tx-DrPaN-8cOUCClMhzPQz9oJmmHXbTmbP00ZepbnwG5t9rsdqM29VnMQWtKqIlitGXRFua5jHqPU2Uh0eQTidCrmxnSXujE-Gzw?key=VJjD-GQ4BeMLFSL3weHQfxOz)

  

Classificação de arestas 

 O tipo de cada aresta pode nos dar informações importantes sobre um grafo. Podemos definir quatro tipos de arestas em termos da floresta produzida:

1. Arestas de Árvore: Quando a DFS descobre um novo vértice v pela primeira vez a aresta (u,v) é chamada de aresta de árvore.
    
2. Arestas de Retorno: São arestas que conectam um vértice u de volta a um de seus ancestrais. Se você encontrar uma aresta (u,v) e v já foi descoberto, mas ainda não foi completamente explorado, essa aresta é de retorno.
    
3. Arestas Diretas: São arestas que conectam um vértice u a um descendente v que já foi explorado. Se você encontrar uma aresta (u,v) e v já foi descoberto, finalizado e é descendente de u, essa aresta é direta.
    
4. Arestas Cruzadas: Se você encontrar uma aresta (u,v) e v já foi descoberto, finalizado, mas v não é descendente de u, essa aresta é cruzada.

    

  
  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfZhFKu1Xw9fNFHRlPLFFWsJYNyMtnX8RZB8OFh-phhPyJjcmme7KA0iu7T5hPdFSAnQNBY_yzGSq2OYW-0IhYWXMlQDx8Mr6xPIWJp9h9j7f8fPYvlImppBpGIqF3QrKKDj5-0yw?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Back edge(B); Forward edge(F); Cross edge(C).

  

___________________________________________________________________________

### 1.4 Ordenação topológica 

 Uma ordenação topológica é uma ordenação dos vértices em um grafo acíclico direcionado, de forma que, se houver um caminho de vi para vj, então vj aparece após vi na ordenação. Normalmente são usados para indicar precedência entre eventos.

 O grafo da figura representa a estrutura de pré-requisitos de cursos em uma universidade. Uma aresta direcionada (v, w) indica que o curso v deve ser completado antes de o curso w ser iniciado.  Fica claro que uma ordenação topológica não é possível se o grafo tiver um ciclo, pois para dois vértices v e w no ciclo, v precede w e w precede v. 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXduA7QuQ1r-dcE6eEiLm4JS-NU74976Miqes7pBha8Ge_PGxN0-Y122pYekxAgO1lG3jdwIN-Lgb5EB7jO4vVbhhFvlDuHur18ZsfIS_S0XumEbMr0BzcXfkYBIkHI4uRFrBkVWCA?key=VJjD-GQ4BeMLFSL3weHQfxOz)

  
  
  

