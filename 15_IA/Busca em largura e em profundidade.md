
#Concluded 

---
### 1. Busca em Largura (BFS - Breadth-First Search)

A Busca em Largura é um algoritmo que explora as arestas de um grafo $G(V,A)$ para "descobrir" todos os vértices alcançáveis a partir de um vértice de origem $s \in V$.

A sua propriedade fundamental é que ela descobre todos os vértices a uma distância $k$ de $s$ antes de descobrir quaisquer vértices a uma distância $k+1$.

Para isso, a BFS utiliza uma estrutura de dados do tipo **Fila (Queue)**.

---
### 2. Busca em Profundidade (DFS - Depth-First Search)

A Busca em Profundidade é um algoritm que explora o mais fundo possível ao longo de cada ramo antes de retroceder.

A estratégia da DFS, ao contrário da BFS, é sempre expandir o vértice "mais novo" (o último descoberto) na fronteira. Assim que um vértice $u$ é descoberto, a DFS explora iterativamente a partir de $u$, e só retorna para explorar outras arestas de $u$ quando toda a exploração descendente de $u$ estiver completa.

Para isso, a DFS utiliza uma estrutura de dados do tipo **Pilha (Stack)**

---
### 3. Exemplo: Mapa de cidades

Queremos descobrir um caminho de Arad para qualquer uma das outras cidades.
![](attachments/Pasted%20image%2020251031091210.png)

**Busca em largura**
```python
from collections import deque
import typing
# Para Busca em Largura: append() e popleft() (FILA)
# Para Busca em Profundidade: append() e pop() (PILHA)

def BUSCA(problema):
    no_inicial = problema.get_estado_inicial()
   
    # A borda contem os nós que o algoritmo já descobriu mas não explorou 
	borda: typing.Deque[No] = deque()
	borda.append(noInicial)
	
	explorados = set() # Conjunto de nós ja explorados

    while True:
        if not borda: # Se não tiver nós na borda
            return
        no_atual = borda.popleft() # remover um nó da borda

        # Se o nó atual for o alvo, retorne a solução
        if problema.is_objetivo(no_atual.estado):
            return no_atual 

        explorados.add(no_atual.estado) # Adicionar nó a explorados.

        # "Para cada sucessor do nó..." 
        for sucessor in problema.sucessores(no_atual):
            if (sucessor not in explorados) and (sucessor not in borda):
                borda.append(sucessor)
```

**Busca em profundidade**
```python
from collections import deque
import typing
# Para Busca em Largura: append() e popleft() (FILA)
# Para Busca em Profundidade: append() e pop() (PILHA)

def BUSCA(problema):
    no_inicial = problema.get_estado_inicial()
   
    # A borda contem os nós que o algoritmo já descobriu mas não explorou 
	borda: typing.Deque[No] = deque()
	borda.append(noInicial)
	
	explorados = set() # Conjunto de nós ja explorados

    while True:
        if not borda: # Se não tiver nós na borda
            return
        no_atual = borda.pop() # remover um nó da borda

        # Se o nó atual for o alvo, retorne a solução
        if problema.is_objetivo(no_atual.estado):
            return no_atual 

        explorados.add(no_atual.estado) # Adicionar nó a explorados.

        # "Para cada sucessor do nó..." 
        for sucessor in problema.sucessores(no_atual):
            if (sucessor not in explorados) and (sucessor not in borda):
                borda.append(sucessor)
```