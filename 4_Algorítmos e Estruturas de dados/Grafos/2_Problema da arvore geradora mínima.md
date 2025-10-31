
#Concluded 

---
### 1. Árvore
Uma árvore é um **grafo conexo e acíclico**; Se é conexo, para qualquer par de vértices do grafo, existe pelo menos um caminho ligando esses dois vértices. Se é acíclico, o grafo não possui ciclos.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfWMRbyy5wl6gMQzlBRe4Pf-V2yG7RZm2M6OhNHSDLYXPtRSoArFEtENF1jrQGiOGT7ewIuBCGP7-IcGM39CugcEXywvXXcIUftsfdszB0DuADVtLnzbrNT_LhY-0dxjRFIaiktXg?key=VJjD-GQ4BeMLFSL3weHQfxOz)


1. Em uma árvore, a quantidade de arestas(E) é o número de vértices(V) - 1. <mark style="background: #ADCCFFA6;">|E|=|V| - 1.</mark>
    
2. Se removermos uma aresta da árvore, ela deixa de ser conexa. Ou seja, <mark style="background: #ADCCFFA6;">uma árvore é um grafo onde os vértices estão minimamente conectados.</mark>
    
3. Se T for árvore, ao adicionarmos uma nova aresta, criamos um ciclo em T. E podemos criar uma nova árvore ao removermos uma aresta do ciclo, diferente da aresta adicionada.

---
### 2. Subgrafo e subgrafo gerador

**Subgrafo**: Se $G′ = (V′ , E′ )$ for subgrafo de um grafo $G = (V, E)$, então $V′ ⊆ V e E′ ⊆ E$.

**Subgrafo gerador**: Um subgrafo $G′ = (V′ , E′ )$ é gerador quando $V′ = V$ e $E′ ⊆ E$. Eles são ditos geradores, por que a partir deles é possível retornar ao grafo original somente adicionando arestas.

Exemplos de subgrafos geradores. 
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcP097izxYt702KbZySGfpYR3sAjf9lVPr3muZFdtuB_bsktVnlUvBM65aBB8qxBk6FbplE5XQmJfg-SMsd7JCSSX3NxUQc7MJVJDb-8akqB1U3hObN49wDBX-Igid7TsVjEj62?key=VJjD-GQ4BeMLFSL3weHQfxOz)



  
  

 Seja um grafo G = (V, E) conexo e ponderado. No problema da árvore geradora mínima, deseja-se encontrar a árvore geradora T de peso mais baixo. O peso de uma árvore geradora é o somatório de todos os pesos associados a uma aresta.

  
  