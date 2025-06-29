
| **Característica**    | **ArrayList**                                                  | **LinkedList**                                                      |
| --------------------- | -------------------------------------------------------------- | ------------------------------------------------------------------- |
| **Tipo de estrutura** | Baseada em array dinâmico                                      | Baseada em lista duplamente encadeada                               |
| **Acesso por índice** | `O(1)`                                                         | `O(n)`, pois precisa percorrer a lista                              |
| **Inserção/rem.**     | `O(n)` pois elementos devem ser deslocados                     | Rápida (`O(1)` para inserção/rem. nas extremidades, `O(n)` no meio) |
| **Uso recomendado**   | Quando há muitas leituras e pouco uso de inserção/rem. no meio | Quando há muitas inserções/remoções em posições variadas            |
### Métodos comuns

| **Método**            | **Descrição**                                     | **Exemplo**             |
| --------------------- | ------------------------------------------------- | ----------------------- |
| `add(E e)`            | Adiciona ao final da lista                        | `lista.add("A");`       |
| `add(int index, E e)` | Adiciona em posição específica                    | `lista.add(1, "B");`    |
| `get(int index)`      | Retorna o elemento da posição                     | `lista.get(0);`         |
| `set(int index, E e)` | Substitui o elemento na posição                   | `lista.set(0, "Novo");` |
| `remove(int index)`   | Remove o elemento da posição                      | `lista.remove(1);`      |
| `remove(Object o)`    | Remove a primeira ocorrência do objeto            | `lista.remove("A");`    |
| `size()`              | Retorna o número de elementos                     | `lista.size();`         |
| `contains(Object o)`  | Verifica se a lista contém um elemento            | `lista.contains("X");`  |
| `clear()`             | Remove todos os elementos                         | `lista.clear();`        |
| `isEmpty()`           | Verifica se a lista está vazia                    | `lista.isEmpty();`      |
| `indexOf(Object o)`   | Retorna o índice da primeira ocorrência do objeto | `lista.indexOf("B");`   |
### Diferenças específicas

| **Operação**                     | **ArrayList**                   | **LinkedList**                          |
| -------------------------------- | ------------------------------- | --------------------------------------- |
| `removeFirst()` / `removeLast()` | **Não disponível diretamente**  | Sim, métodos específicos para isso      |
| `addFirst(E e)` / `addLast(E e)` | **Não disponível diretamente**  | Sim, permite uso como fila ou pilha     |
| **Uso como fila (Queue)**        | Não recomendado                 | Sim, implementa `Deque` e `Queue`       |
| **Consumo de memória**           | Menor, por ser baseado em array | Maior, pois armazena referências extras |

---

Se quiser, posso fornecer um exemplo de código simples comparando o uso de ambas também.