
Observe o seguinte problema. Dado o mapa abaixo, eu quero descobrir caminhos de Arad para qualquer
![](attachments/Pasted%20image%2020251031091210.png)



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