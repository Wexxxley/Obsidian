
| **Característica**    | **ArrayList**                                          | **LinkedList**                                           |
| --------------------- | ------------------------------------------------------ | -------------------------------------------------------- |
| **Tipo de estrutura** | Baseada em array dinâmico                              | Baseada em lista duplamente encadeada                    |
| **Acesso por índice** | `O(1)`                                                 | `O(n)`, pois precisa percorrer a lista                   |
| **Inserção/rem.**     | `O(n)` pois elementos devem ser deslocados             | `O(1)` nas extremidades                                  |
| **Uso recomendado**   | Quando há muitas leituras e pouco uso de inserção/rem. | Quando há muitas inserções/remoções em posições variadas |
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

| **Operação**                   | **ArrayList**      | **LinkedList**                      |
| ------------------------------ | ------------------ | ----------------------------------- |
| `removeFirst()` `removeLast()` | **Não disponível** | Sim, métodos específicos para isso  |
| `addFirst(e)` `addLast(e)`     | **Não disponível** | Sim, permite uso como fila ou pilha |
