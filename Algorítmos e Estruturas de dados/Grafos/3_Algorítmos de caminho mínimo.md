
---

 Existem variações desse tipo de problema:
- Problema de caminhos mínimos de fonte única; 
- Problema de caminhos mínimos com um só destino; 
- Problema do caminho mínimo para um par; 
- Problema de caminhos mínimos para todos os pares;

 O custo de um caminho v1,v2,...,vN é dado pelo somatório dos custos no caminho​. Se for um grafo não ponderado, o menor caminho será aquele com a menor quantidade de vértices.

---
### **1. Problema do Caminho Mínimo de fonte Única**

- O grafo na figura abaixo mostra os problemas que arestas negativas podem causar. O caminho de v5 para v4 tem custo 1, mas existe um mais curto seguindo v5,v4,v2,v5,v4, com custo −5. Este caminho ainda não é o mais curto, pois poderíamos permanecer nesse ciclo. Isto é conhecido como ciclo de custo negativo; quando há um no grafo, os caminhos mais curtos são indefinidos.
- ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeul46kW9zTZF43lTQxr7MmIe3DA4lhhw5sSSnlaZmZSo2c7JIMDNpV9wvgBCy5VTTxJDYpKSAGI5D5mqjOgGoc8kxkQVDbDYkMYKaicS_BNj4MgHnQir6ueeZvzLu_ogck7YGD?key=VJjD-GQ4BeMLFSL3weHQfxOz)
 - A figura abaixo mostra um grafo ponderado. Gostaríamos de encontrar o caminho mais curto a partir de s para todos os outros vértices. 
  ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfGFaPphwr-tFjkUrYM-R0yb-EtaoMqWG1idOXWypr-mz81XVxhq_XsEhBlTpXRS6PHh0gZUOlZHwV2RnRnnVns9V2aQOqLQR3Aq3CA7hC1OGS2hgJtNSXGr08lmuVK9LZ-f6PrvA?key=VJjD-GQ4BeMLFSL3weHQfxOz)
  - Suponha que escolhemos s como v3. Agora, podemos começar a procurar todos os vértices que estão a uma distância 1. Se fizermos isso, veremos que podemos agora encontrar vértices cujo caminho mais curto de s é 2. Podemos encontrar, então, os com distância 3. 

Essa estratégia é conhecida como busca em largura. Ela opera processando vértices em camadas. Dada essa estratégia, precisamos traduzi-la em código.   
___
#### **1.2 Algoritmo de Dijkstra**
 O método geral para resolver o problema do menor caminho com origem única é conhecido como algoritmo de Dijkstra. Só pode ser usado com grafos sem peso negativo.  Primeiro iniciamos cada vértice com pai nulo e distância infinita, exceto s com distancia 0. Depois é aplicado a técnica do relaxamento.   
 
**Técnica do relaxamento**: O propósito de relaxar uma aresta (u, v) consiste em testar se podemos melhorar a estimativa do caminho mais curto para v encontrado até então, por meio do caminho passando por u. 
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdRKHY_7z8OOBsb-SRQtAIQNYd4SvGupvQBGl1noonqGyZKEueEyt1nk1HL9z-jBufixQJAFP4WlrmhwOBsKBul2KnKpXzwzlE8FaRcfo6v0Odxf7idUBaD0kwXJBjacblG_ITVFw?key=VJjD-GQ4BeMLFSL3weHQfxOz)

``` cpp title:test.cpp
void dijkstra(G, s) {
    for each Vertex v in G.Vertices {
        v.dist = INFINITY; // Inicializa a distância de todos os vértices como infinito
        v.pai = null;      // Inicializa o predecessor de todos os vértices como nulo
    }
    s.dist = 0; // A distância do vértice de partida 's' para si mesmo é 0

    // 2. Criação da Fila de Prioridade Mínima (Q)
    // Q contém todos os vértices do grafo, priorizados por sua 'dist' atual
    Q = new MinPriorityQueue(G.Vertices); 

    // 3. Loop principal: Processa os vértices em ordem de distância crescente
    while (Q is not empty) {
        // Extrai o vértice 'v' com a menor distância atual de 's'
        Vertex v = Q.ExtractMin(); 

        // 4. Relaxamento das arestas: Atualiza as distâncias dos vizinhos de 'v'
        for each Vertex w adjacent to v {
            int custo = cost of edge (v, w); // Obtém o custo da aresta de v para w

            // Se um caminho mais curto para 'w' for encontrado através de 'v'
            if (v.dist + custo < w.dist) {
                w.dist = v.dist + custo; // Atualiza a distância de 'w'
                w.pai = v;               // Define 'v' como predecessor de 'w' no caminho mais curto
                // Opcional: Se 'Q' suportar, chamar Q.DecreaseKey(w, w.dist) para atualizar sua prioridade
            }
        }
    }
}
```

*
  

|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1 void dijkstra(G, s) {<br><br>2     for each Vertex v {<br><br>3         v.dist = INFINITY; <br><br>4         v.pai = null;<br><br>5     }<br><br>6     s.dist = 0; <br><br>7<br><br>8     Q = new Q{G.Vertices}; // fila de prioridade mínima<br><br>9     while (Q =! empty)  {<br><br>10        Vertex v = Q.ExtractMin();//extrai o com menor dist<br><br>11<br><br>12        for each Vertex w adjacent to v  {<br><br>12            int custo = custo da aresta (v,w);<br><br>14            if (v.dist + custo < w.dist)  {<br><br>15                    w.dist =  v.dist + custo;<br><br>16                    w.pai = v;<br><br>17            }<br><br>18        }<br><br>19    }<br><br>20} |

  

 Q armazena os vértices do grafo que ainda não foram processados. Ela é organizada como uma fila de prioridade mínima, ou seja, os vértices com a menor distância são extraídos primeiro.

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeXJfxWiIfoAjoaXmShVu6pGuNf87iw1IBv8gWEUCMLr1n1cNt5gYGkKnQ4SX_D7A78T74rabIHqsAuWkeGJUhnZrlBUSj7jGoT71BccauO2jfWOfeZ6ST3aF9vaO0ylfiKdT4W7w?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Ordem de execução começando de v1

  
  
  
  
  