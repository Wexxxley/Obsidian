
![](attachments/Pasted%20image%2020251031091210.png)



```python
from collections import deque
# Para Busca em Largura: append() e popleft() (FILA)
# Para Busca em Profundidade: append() e pop() (PILHA)

def BUSCA(problema):
    no_inicial = problema.get_estado_inicial()
   
    # Ab borda representa nós que o algoritmo já descobriu 
    # mas ainda não explorou.    
	borda: typing.Deque[No] = deque()
	borda.append(noInicial)
	
	# Conjunto de nós ja explorados
	explorados = set()

    while True:
	    # Se não tiver nós na borda
        if not borda:
            return

        # remover um nó da borda
        no_atual = borda.popleft() 

        # Se o nó atual for o alvo, retorne a solução
        if problema.is_objetivo(no_atual.estado):
            return no_atual 

        # Adicionar nó a explorados.
        explorados.add(no_atual.estado)


        # (Esta linha geralmente significa: "Para cada sucessor do nó...") 
        for acao, proximo_estado in problema.sucessores(no_atual.estado):
            
            # "...se o estado do sucessor não estiver em explorados OU na borda"
            if proximo_estado not in explorados and proximo_estado not in estados_na_borda:
                
                # Criar o nó sucessor
                no_sucessor = criar_no(proximo_estado, pai=no_atual, acao=acao)
                
                # Adicionar o sucessor na borda
                borda.append(no_sucessor)
                estados_na_borda.add(proximo_estado)
        
        # 10. } (Fim do loop while)
```