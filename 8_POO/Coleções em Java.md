
---

### **Array**
O arryay armazena um número fixo de elementos de um mesmo tipo, seja primitivo (int, double) ou um objeto.
- **Tamanho Fixo**
- **Acesso por índice:** ``meuArray[0] ``extremamente rápido.
- **Performance:** Por ter um tamanho fixo e ser uma estrutura simples, é muito eficiente em termos de memória e velocidade.

```java
String[] nomes = new String[3];

nomes[0] = "Matheus";
nomes[1] = "João";
nomes[2] = "Julia";

System.out.println("O segundo nome é: " + nomes[1]); 


// Tentando adicionar um quarto elemento causa um erro ()
// nomes[3] = "David"; 
```

- Caso você tente 

---

### ArrayList

O `ArrayList` é uma das implementações da interface `List` e é a mais popular. Pense nele como um `Array` dinâmico: ele armazena elementos em uma estrutura interna de array, mas **aumenta ou diminui de tamanho automaticamente** conforme necessário.

- **Tamanho Dinâmico:** Você pode adicionar ou remover elementos sem se preocupar com o tamanho.
    
- **Acesso Rápido:** Assim como um array, o acesso por índice é rápido.
    
- **Inserção/Remoção Lenta no Meio:** Adicionar ou remover um elemento no meio da lista é mais lento, pois todos os elementos seguintes precisam ser movidos.
    

#### Código de Exemplo:

Java

```
import java.util.ArrayList;

ArrayList<String> frutas = new ArrayList<>();

frutas.add("Maçã");
frutas.add("Banana");
frutas.add("Abacaxi"); // O ArrayList cresce automaticamente

System.out.println("A primeira fruta é: " + frutas.get(0));
// Saída: A primeira fruta é: Maçã

// Inserindo no meio, todos os elementos após "Maçã" são deslocados
frutas.add(1, "Laranja"); 

System.out.println(frutas);
// Saída: [Maçã, Laranja, Banana, Abacaxi]
```

---

### LinkedList

O `LinkedList` é outra implementação da interface `List`. Diferente do `ArrayList`, ele não usa um array interno. Ele armazena os elementos em **nós**, onde cada nó guarda o valor e uma referência para o nó anterior e o próximo.

- **Estrutura de Nós:** Cada elemento é um "nó" que se conecta aos seus vizinhos.
    
- **Inserção/Remoção Rápida:** Adicionar ou remover um elemento é muito rápido, pois envolve apenas a mudança de algumas referências (ponteiros), sem precisar deslocar outros elementos.
    
- **Acesso Lento:** Acessar um elemento por índice (ex: `get(5)`) é mais lento, pois o Java precisa percorrer a lista a partir do início ou do fim para chegar até o elemento desejado.
    

#### Código de Exemplo:

Java

```
import java.util.LinkedList;

LinkedList<String> tarefas = new LinkedList<>();

tarefas.add("Estudar Java");
tarefas.add("Fazer compras");
tarefas.add("Pagar contas");

// Adicionando um elemento no meio da lista, uma operação muito rápida para LinkedList
tarefas.add(1, "Lavar o carro"); 

System.out.println(tarefas);
// Saída: [Estudar Java, Lavar o carro, Fazer compras, Pagar contas]

// Acessar por índice é menos eficiente
System.out.println("A segunda tarefa é: " + tarefas.get(1));
// Saída: A segunda tarefa é: Lavar o carro
```

---



### Quando Usar Cada Um?

| Característica               | `Array`                                          | `ArrayList`                                                          | `LinkedList`                                                   |
| ---------------------------- | ------------------------------------------------ | -------------------------------------------------------------------- | -------------------------------------------------------------- |
| **Tamanho**                  | Fixo                                             | Dinâmico (cresce automaticamente)                                    | Dinâmico (cresce automaticamente)                              |
| **Acesso por Índice**        | **Muito rápido**                                 | **Muito rápido**                                                     | Lento (precisa percorrer a lista)                              |
| **Inserção/Remoção no Meio** | Impossível                                       | Lenta (desloca elementos)                                            | **Muito rápida** (muda referências)                            |
| **Melhor Uso**               | Quando o número de elementos é conhecido e fixo. | Quando precisa de acesso rápido e poucas inserções/remoções no meio. | Quando precisa de muitas inserções/remoções no meio ou início. |
|                              |                                                  |                                                                      |                                                                |

# LinkedList vs ArrayList (JAVA)

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

![](attachments/Pasted%20image%2020250815093252.png)