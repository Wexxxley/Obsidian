
#Concluded 

---
Esses algoritmos utilizam uma **função heurística** $h(n)$ que estima o custo do nó $n$ até o objetivo. Isso permite que o algoritmo "corte caminho" no espaço de busca, priorizando nós que parecem promissores.
### Busca gulosa
Tenta expandir o nó que está mais perto do objetivo, ignorando o custo já pago para chegar até ali.

- Não é ótima. Por ignorar o custo de deslocamento, ela pode escolher um caminho visualmente curto, mas custoso.        

![](../attachments/Pasted%20image%2020251204153017.png)

### Busca estrela

A prioridade é a soma do custo real com a heurística: (custoCaminho + heuristica, new_no).
![](../attachments/Pasted%20image%2020251204153227.png)

