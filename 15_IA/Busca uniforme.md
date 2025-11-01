

---


```python
import heapq  # Biblioteca para Fila de Prioridade
import typing

# --- DEFINIÇÃO DO NÓ ---
# Para a Busca de Custo Uniforme, o Nó é essencial
# Ele precisa guardar o custo e ser comparável (para a fila de prioridade)

class No:
    def __init__(self, estado, pai, custoCaminho):
        self.estado = estado
        self.pai = pai
        self.custoCaminho = custoCaminho
    
    # Define como comparar dois nós (baseado no menor custo)
    # Isso é o que faz o heapq funcionar.
    def __lt__(self, other):
        return self.custoCaminho < other.custoCaminho

# --- FUNÇÃO DE BUSCA ---

def BUSCA_CUSTO_UNIFORME(problema):
    # (Linha 02)
    # Assumimos que o problema.get_estado_inicial() retorna um Nó
    # com estado inicial, pai=None e custoCaminho=0
    no_inicial = problema.get_estado_inicial() 
    
    # A borda agora é uma Fila de Prioridade (um heap).
    # É uma lista gerenciada pelo 'heapq'.
    borda: typing.List[No] = []
    heapq.heappush(borda, no_inicial)
    
    explorados = set() # Conjunto de ESTADOS ja explorados

    # (Linha 03) repita
    while True:
        # (Linha 04) se borda está vazia retorne falha
        if not borda: 
            return None # Falha
        
        # (Linha 05) nó ← remover elemento da borda (com MENOR custo)
        no_atual = heapq.heappop(borda) 

        # (Linha 06) se nó.estado é objetivo retorne solução
        if problema.is_objetivo(no_atual.estado):
            return no_atual 

        # (Linha 07) adicionar nó.estado a explorados
        # Importante: só adiciona em explorados QUANDO o nó é selecionado.
        if no_atual.estado not in explorados:
            explorados.add(no_atual.estado)

            # (Linha 09) para cada ação aplicável...
            # (Linha 10) filho ← criar nó filho
            # Assumimos que 'sucessores' retorna Nós (estado, pai, custoCaminho)
            for sucessor in problema.sucessores(no_atual):
                
                # (Linhas 11-14)
                # Se o estado do sucessor ainda não foi explorado...
                # (A lógica de "substituir se custo for maior" é
                # tratada automaticamente pelo 'explorados' e pela
                # ordem de saída da fila de prioridade)
                if sucessor.estado not in explorados:
                    # (Linha 12) adicionar filho em borda
                    heapq.heappush(borda, sucessor)
```