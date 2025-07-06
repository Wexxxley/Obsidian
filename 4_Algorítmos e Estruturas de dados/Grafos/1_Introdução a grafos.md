
---
## **1 Grafos**

 Um grafo ==G = (V, E)== consiste em um ==conjunto de vértices (V)== e um ==conjunto de arestas (E)==. Cada aresta é um par (v,w),  onde v,w ∈ V.

 - Se o par tiver direção, o grafo é **direcionado**. 
 - O vértice w é adjacente a v se, e somente se, (v,w) ∈ E. 
 - Em um **grafo não direcionado** com a aresta (v,w) e, consequentemente, (w,v), w é adjacente a v e v é adjacente a w. Às vezes, uma aresta tem um terceiro componente, conhecido como **peso**.
 - Um **caminho** em um grafo é uma sequência de vértices w1,w2,w3,…,wN tal que (wi,wi+1) ∈ E, ou seja, são adjacestes. Permitimos um caminho de um vértice para ele mesmo (loop); 
 - Um grafo **não direcionado** é **conexo** se houver um caminho de qualquer vértice para qualquer outro vértice. Um grafo **direcionado** com essa propriedade é chamado de fortemente conexo.
 - Se um grafo direcionado não for fortemente conexo, mas o **grafo subjacente (sem considerar a direção dos arcos)** for conexo, então o grafo é dito fracamente conexo. 
 - Um grafo completo é um grafo em que existe uma aresta entre cada par de vértices.

Um ==**grafo G = (V, E)**== é composto por um **conjunto de vértices (V)** e um **conjunto de arestas (E)**. Cada aresta é definida por um par de vértices (v, w), onde v e w pertencem a V.

- Se o par de vértices que define a aresta **indica uma direção**, o grafo é **direcionado**.
- O vértice _w_ é **adjacente** a _v_ se, e somente se, existe uma aresta _(v, w)_ em E.
- Em um **grafo não direcionado**, se existe uma aresta _(v, w)_, então implicitamente também existe _(w, v)_. Nesse caso, _w_ é adjacente a _v_, e _v_ é adjacente a _w_.
- Opcionalmente, uma aresta pode ter um terceiro componente, chamado **peso** (ou custo).
- Um **caminho** em um grafo é uma sequência de vértices w1​,w2​,w3​,…,wN​ tal que, para cada i de 1 a N−1, a aresta (wi​,wi+1​) pertence a E. Isso significa que vértices consecutivos no caminho são adjacentes. Um caminho pode começar e terminar no mesmo vértice (formando um _ciclo_).
- Um grafo **não direcionado** é **conexo** se existe um caminho entre qualquer par de vértices.
- Um grafo **direcionado** é **fortemente conexo** se existe um caminho de qualquer vértice para qualquer outro vértice, seguindo as direções das arestas.
- Se um grafo **direcionado** não é fortemente conexo, mas seu **grafo subjacente** (o mesmo grafo sem considerar a direção das arestas) é conexo, então ele é chamado de **fracamente conexo**.
- Um **grafo completo** é um grafo no qual existe uma aresta entre cada par de vértices distintos.

___
### **1.1 Representação de grafos**

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfH6clvRtr8C23J8Ff5Hq-LOek1BcgvQ7StRsr3FmFQiLs1i_-vgQJWCJBnUY7vs-7SJSnKZZ4f9EsjekLAO7UgKKkUe5X08iaNu5_H1E89xEHhlyJuxiU_-_cbzcRHNm-suELs?key=VJjD-GQ4BeMLFSL3weHQfxOz)

#### **1.1.1 Matriz de Adjacência**

Para um grafo com N vértices, a matriz de adjacência é uma matriz quadrada N×N.

- Para cada aresta (u,v), a entrada `A[u][v]` é definida como `verdadeiro`(`1`).
- Caso contrário, a entrada será `falsa`(`0`).
- Se a aresta tiver um **peso** associado, `A[u][v]` pode armazenar esse peso. Nesse caso:
    - Um valor muito grande (∞) pode indicar a inexistência de uma aresta.

**Desvantagens da Matriz de Adjacência:**
- Embora seja **simples** de entender e implementar, é **muito ineficiente** em termos de espaço.
- Isso ocorre porque, em **grafos esparsos** (aqueles com relativamente poucas arestas em comparação com o número máximo possível de arestas), a maioria dos valores na matriz será nula, resultando em **desperdício de memória**.

#### **1.1.2 Listas de Adjacência**

Uma solução melhor para **grafos não densos (esparsos)** é o uso de listas de adjacência.

- Para cada vértice v, mantemos uma **lista de todos os vértices adjacentes** a ele.
- As listas de adjacência são o **padrão** para representar grafos na maioria das aplicações.
- Em **grafos não direcionados**, cada aresta (u,v) aparecerá em duas listas: v estará na lista de adjacência de u, e u estará na lista de adjacência de v.

  
___________________________________________________________________________

___________________________________________________________________________

### 1.5 Problema da árvore geradora mínima![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfWMRbyy5wl6gMQzlBRe4Pf-V2yG7RZm2M6OhNHSDLYXPtRSoArFEtENF1jrQGiOGT7ewIuBCGP7-IcGM39CugcEXywvXXcIUftsfdszB0DuADVtLnzbrNT_LhY-0dxjRFIaiktXg?key=VJjD-GQ4BeMLFSL3weHQfxOz)

  Uma árvore é um grafo conexo e acíclico; Se é conexo, para qualquer par de vértices do grafo, existe pelo menos um caminho ligando esses dois vértices. Se é acíclico, o grafo não possui ciclos.

  

1. Em uma árvore, a quantidade de arestas(E) é o número de vértices(V) - 1. |E|=|V| - 1.
    
2. Se removermos uma aresta da árvore, ela deixa de ser conexa. Ou seja, uma árvore é um grafo onde os vértices estão minimamente conectados.
    
3. Se T for árvore, ao adicionarmos uma nova aresta, criamos um ciclo em T. E podemos criar uma nova árvore ao removermos uma aresta do ciclo, diferente da aresta adicionada.
    

  

Subgrafo e subgrafo gerador

Subgrafo: Se G′ = (V′ , E′ ) for subgrafo de um grafo G = (V, E), então V′ ⊆ V e E′ ⊆ E.

Subgrafo gerador: Um subgrafo G′ = (V′ , E′ ) é gerador quando V′ = V e E′ ⊆ E. Eles são ditos geradores, por que a partir deles é possível retornar ao grafo original somente adicionando arestas.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcP097izxYt702KbZySGfpYR3sAjf9lVPr3muZFdtuB_bsktVnlUvBM65aBB8qxBk6FbplE5XQmJfg-SMsd7JCSSX3NxUQc7MJVJDb-8akqB1U3hObN49wDBX-Igid7TsVjEj62?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Exemplos de subgrafos geradores. 

  
  

 Seja um grafo G = (V, E) conexo e ponderado. No problema da árvore geradora mínima, deseja-se encontrar a árvore geradora T de peso mais baixo. O peso de uma árvore geradora é o somatório de todos os pesos associados a uma aresta.

  
  
  

___________________________________________________________________________

#### 1.5.1 Algoritmo de Kruskal 

 Para o problema da árvore geradora mínima, o algoritmo começa com todos os vértices e sem nenhuma aresta. De forma iterativa, seleciona uma aresta com o menor peso para ser adicionada de modo que não gere ciclo com as arestas já escolhidas. O algoritmo para ao selecionar a quantidade máxima de arestas de uma árvore, que é |E|=|V| - 1.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfkH05cmMQP2Z-Kn_5UtsSDsdGQyw3yPS_9EjzOpfF4uqXG2pXiZ7DHGQBX7mqpd5nyQAaoLUN_rCXcHb9ULvf-WCMEB38s43eFcD-aNpfGQpeUSL6eqIi2X0NdnYpVCLABXjMm0g?key=VJjD-GQ4BeMLFSL3weHQfxOz)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd4RExmUmQBk-tUAsFpIUhmGc0avx57lfdjkhCRhDsQD3QhrIR-gJPNZ46K1SGidKiMwMD--RqvhhoBW6gDm_q9pxbHkQi5KmLhvVM9xzwNMZea8vBKlSTLoHmKg5F5hWE_oTfIfw?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Grafo original e sua árvore geradora mínima.

  

 Imagine os vértices sem nenhuma aresta. Primeiro, o algoritmo seleciona a aresta com peso 1, de modo a não gerar ciclo. Depois qualquer uma das duas arestas com peso 2, e depois a segunda aresta com peso 2. Depois qualquer uma das duas arestas com peso 4, depois a outra aresta com peso 4. O 6 ele não pode selecionar, pois gera ciclo. Esse processo continua até selecionar o limite de arestas.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf6NN2L4QOSrl-eCXJSyJcHjiohTkJaz1GxPZCfKmCwKH6DS8vePEln5AHKeqYL9m85hpNNFN6uVf-O_oY-qx3esanFK4trc3HQHRX9N086gB5SqtlnDm7_C_ILzr9LGYt-cZBF5Q?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Pseudocódigo de Kruskal.

  

 Primeiro é inicializado o conjunto A, onde será armazenado as arestas da árvore geradora mínima. Depois são criadas |V| árvores, cada uma com um vértice. 

 O laço for das linhas 5-8 examina arestas em ordem de peso, do mais baixo ao mais alto. O laço verifica, para cada aresta (u, v), se u e v pertencem à mesma árvore. Se pertencerem, então a aresta (u, v) não pode ser adicionada, pois criaria um ciclo. Do contrário, os dois vértices pertencem a árvores diferentes. Nesse caso, a linha 7 adiciona a aresta a A e a linha 8 une os dois conjuntos que possuem u e v. O algoritmo utiliza a estrutura conjuntos disjuntos para representar a floresta. 

  

Conjuntos disjuntos

  Uma estrutura de conjuntos disjuntos mantém uma coleção S = {S1 , S2 , ..., Sk} de conjuntos disjuntos. Identificamos cada conjunto por um representante, que é algum membro do conjunto. Em algumas aplicações, não importa qual membro seja usado como representante. Outras aplicações podem exigir uma regra para escolher o representante.Desejamos suportar as seguintes operações: 

  

1. MAKE-SET(x): cria um novo conjunto cujo único membro é x. Visto que os conjuntos são disjuntos, exigimos que x ainda não esteja em outro conjunto.
    
2. UNION(x, y): une os conjuntos que contêm x e y. Supomos que os dois conjuntos são disjuntos antes da operação.
    
3. FIND-SET(x): retorna um ponteiro para o representante do único conjunto que contém x. 
    

  

___________________________________________________________________________

#### 1.5.2 Algoritmo de Prim

 Primeiro é importante conhecer o conceito de corte de um grafo: Dado um grafo G=(V,E), um corte é uma partição do conjunto de vértices V em dois subconjuntos S e V - S.![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfML2G_rZQku82DAyHZzDswGakwGvX_VkexwURkns6k0Qm38yAcE_ptGlz0B7Wy3jmUABE4kTxAQ1iJ7Kv6HyAHd7WY8PI8KLz2coSfdYZ9slb-0kBrZz2Xgem8gHJbIOe_Uo_94Q?key=VJjD-GQ4BeMLFSL3weHQfxOz)

O conjunto de arestas que cruzam o corte são aquelas que têm um extremo em S e o outro em V - S.

  

 No algoritmo de prim, esse conceito de corte é usado para decidir quais arestas podem ser adicionadas à árvore geradora mínima. 

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfJCCh5dFoRLi0Lfvl1G1anKTXWjM7Q_sGjTGIn724_TkhUf7eQReH7WzR7W_Ikz7gvsnsiVeoN2eUdmDGolv9M4Ao4pw93dhZZE7Q_gwW_TxaD_n53DpuxRuBE-v80mP5oF7ZxHA?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Pseudocódigo do algoritmo de Prim. 

Cada vértice do grafo é inicializado: 

- u.key  = infinity: representa o custo para incluir o vértice na árvore.
    
- u.pai = null: indica que o vértice ainda não foi conectado à árvore.
    

  

 Depois é definido r.key = 0, pois ele é o vértice inicial. Então, é criado Q com todos os vértices. Q é uma fila de prioridade, ou seja, os elementos com as menores chaves são retirados primeiro.

  

 Temos um loop nas linhas 6-11. Enquanto a fila não for vazia é retirado o vértice u com menor chave. Para cada vétice u retirado da fila, é feito um for com cada vértice v adjacente a u. Então, cada vértice adjacente a u tem seu pai e peso atualizado. Após verificar todos os vértices adjacentes a u o for acaba e o vértice com menor peso da fila é retirado. O processo se repete até a fila estar vazia.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcSx2XwO8LWqzqZnnxM6PiGIYrN9AslE7tf0w26OsnYcSDl6RiLaUkDNxY26aA9h_ELymVHql3FvF4_iAqxlWvkIwomSWAfGcgUJOWEfsF4y7v0pOJrHZ_-FkWh0GbUFmfUaWNlxQ?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Passo a passo do algoritmo de Prim.

  

Complexidade

 Ambos Kruskal e Prim são da ordem O(m log n).

  
  
  

___________________________________________________________________________

  
  
  
  
  
  
  
**