Status: #Concluded  

---
# 1. Array

Os arrays em js podem ter qualquer tipo de dado

![Pasted image 20250513162620](../../../attachments/Pasted%20image%2020250513162620.png)

### Tabela Completa de Métodos de Array

==cb = callback==

| Método                | Descrição                                                    | Muta?      |
| --------------------- | ------------------------------------------------------------ | ---------- |
| `forEach(cb)`         | Executa uma função para cada item.                           | 🟢 Não     |
| `map(cb)`             | **Cria um novo array** transformando cada item.              | 🟢 Não     |
| `filter(cb)`          | **Cria um novo array** com itens que passam em um teste.     | 🟢 Não     |
| `find(cb)`            | **Retorna o primeiro item** que passa em um teste.           | 🟢 Não     |
| `findIndex(cb)`       | Retorna o **índice do primeiro item** que passa no teste.    | 🟢 Não     |
| `indexOf(item)`       | Retorna o **primeiro índice** de um item.                    | 🟢 Não     |
| `push(item)`          | **Adiciona** um item ao **final** do array.                  | ⚠️ **Sim** |
| `pop()`               | **Remove** um item do **final** do array.                    | ⚠️ **Sim** |
| `unshift(item)`       | **Adiciona** um item ao **início** do array.                 | ⚠️ **Sim** |
| `shift()`             | **Remove** um item do **início** do array.                   | ⚠️ **Sim** |
| `splice(idx, n, ...)` | **Adiciona, remove ou substitui itens em qualquer posição.** | ⚠️ **Sim** |
