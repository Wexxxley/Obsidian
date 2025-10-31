
  

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
