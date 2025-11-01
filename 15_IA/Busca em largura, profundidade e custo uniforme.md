
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
### 3. Busca de Custo Uniforme (UCS - Uniform Cost Search)

A Busca de Custo Uniforme é um algoritmo que explora o grafo $G(V,A)$ para encontrar o caminho de **menor custo total** (e não apenas o de menor número de arestas) de um vértice de origem $s$ até um vértice de destino.

A sua propriedade fundamental é que ela sempre expande o nó $n$ na fronteira (borda) que tem o **menor custo de caminho total** desde a origem $s$. Por causa disso, a UCS garante encontrar o caminho de menor custo para o destino (desde que os custos das arestas não sejam negativos).

Para isso, a UCS utiliza uma estrutura de dados do tipo **Fila de Prioridade (Priority Queue)**.

---
### 4. Exemplo: Mapa de cidades

Queremos descobrir um caminho de Arad para qualquer uma das outras cidades.
![](attachments/Pasted%20image%2020251031091210.png)

**Busca em largura**
Levando em consideração que "problema" possui a estrutura que salva o mapa e todas as informações necessárias.
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
Levando em consideração que "problema" possui a estrutura que salva o mapa e todas as informações necessárias.
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

**Busca custo uniforme**
Levando em consideração que "problema" possui a estrutura que salva o mapa e todas as informações necessárias.
```python
import heapq  # Biblioteca para Fila de Prioridade (heap)
import typing

def BUSCA_CUSTO_UNIFORME(Problema):
    no_inicial = problema.get_estado_inicial() 
    
    borda: typing.List[No] = []
    heapq.heappush(borda, no_inicial)
    
    explorados = set() # Armazena nomes de estados
    
    while True:
        if not borda: # Se não tiver nós na borda
            return None 
        
        no_atual = heapq.heappop(borda) # remover no da borda (menor path)

        # Se o nó atual for o alvo, retorne a solução
        if problema.is_objetivo(no_atual.estado):
            return no_atual

		# Se já exploramos (com um custo menor), pulamos
		if noAtual.estado.nome in explorados:
			continue
        explorados.add(no_atual.estado.nome) # adicionar no a explorados
        
        # "Para cada sucessor do nó..." 
        for filho in problema.sucessores(no_atual):
            
            # Se filho NÃO está em explorados
            # NÃO precisamos checar se ele está na borda
            if filho.estado.nome not in explorados:
	            filho.dist += no_atual.dist
                heapq.heappush(borda, filho)
```
