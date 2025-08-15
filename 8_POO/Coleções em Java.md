
---
### **Array**
O arryay armazena um número fixo de elementos de um mesmo tipo, seja primitivo (int, double) ou um objeto.
- **Tamanho Fixo**
- **Acesso por índice:** ``meuArray[0] ``extremamente rápido.
- **Performance:** Por ter um tamanho fixo e ser uma estrutura simples, é muito eficiente em termos de memória e velocidade.

```java
String[] nomes = new String[4];

nomes[0] = "Matheus";
nomes[1] = "João";
nomes[3] = "Julia";

System.out.println("O segundo nome é: " + nomes[1]); 
```
![600](attachments/Pasted%20image%2020250815134802.png)
- Caso você tente acessar fora da memoria alocada: **IndexOutOfBoundsException**

---
### **ArrayList**
O `ArrayList` é uma das implementações da interface `List` . É como um `Array` dinâmico: ele armazena elementos em uma estrutura interna de array, mas **aumenta ou diminui de tamanho automaticamente** conforme necessário.
- **Tamanho Dinâmico** 
- **Acesso Rápido** 
- **Inserção/Remoção Lenta no Meio:** Adicionar ou remover um elemento no meio da lista é mais lento, pois todos os elementos seguintes precisam ser movidos.

```java
import java.util.ArrayList;

ArrayList<String> frutas = new ArrayList<String>();

frutas.add("Maçã");
frutas.add("Banana");
frutas.add("Abacaxi"); 

System.out.println("A primeira fruta é: " + frutas.get(0));

// Inserindo no meio, elementos são deslocados
frutas.add(1, "Laranja"); 
```
- No `ArrayList`, quando você remove um elemento, a lista "se compacta" para preencher o espaço. Se você quer manter o espaço vazio, você deve explicitamente colocar o valor `null`.

---
### **LinkedList**
O `LinkedList` é outra implementação da interface `List`. Ele armazena os elementos em **nós**, onde cada nó guarda o valor e uma referência para o nó anterior e o próximo.

- **Estrutura de Nós:** Cada elemento é um nó que se conecta aos seus vizinhos.
- **Inserção/Remoção Rápida:** Adicionar ou remover um elemento é rápido, pois envolve apenas a mudança de algumas referências (ponteiros), sem precisar deslocar outros elementos.
- **Acesso Lento:** Acessar um elemento por índice é mais lento, pois é preciso percorrer a lista a partir do início ou do fim para chegar até o elemento desejado.

```java
import java.util.LinkedList;

LinkedList<String> tarefas = new LinkedList<String>();

tarefas.add("Estudar Java");
tarefas.add("Fazer compras");
tarefas.add("Pagar contas");

// Adicionando um elemento no meio da lista
tarefas.add(1, "Lavar o carro"); 

// Acessar por índice é menos eficiente
System.out.println("A segunda tarefa é: " + tarefas.get(1));
```
- No `LinkedList`, quando você remove um elemento, a lista "se compacta" para preencher o espaço. Se você quer manter o espaço vazio, você deve explicitamente colocar o valor `null`.

---
### **Quando Usar Cada Um?**

| Característica               | `Array`                   | `ArrayList`                               | `LinkedList`                                |
| ---------------------------- | ------------------------- | ----------------------------------------- | ------------------------------------------- |
| **Tamanho**                  | Fixo                      | Dinâmico                                  | Dinâmico                                    |
| **Acesso por Índice**        | Muito rápido              | Muito rápido                              | Lento                                       |
| **Inserção/Remoção no Meio** | Impossível                | Lenta (desloca elementos)                 | Rápida(muda referências)                    |
| **Melhor Uso**               | Número de elementos fixo. | Acesso rápido e poucas operacoes no meio. | Quando precisa de muitas operacoes no meio. |

---
### **LinkedList vs ArrayList** 

| **Característica**    | **ArrayList**                                          | **LinkedList**                                           |
| --------------------- | ------------------------------------------------------ | -------------------------------------------------------- |
| **Tipo de estrutura** | Baseada em array dinâmico                              | Baseada em lista duplamente encadeada                    |
| **Acesso por índice** | `O(1)`                                                 | `O(n)`, pois precisa percorrer a lista                   |
| **Inserção/rem.**     | `O(n)` pois elementos devem ser deslocados             | `O(1)` nas extremidades                                  |
| **Uso recomendado**   | Quando há muitas leituras e pouco uso de inserção/rem. | Quando há muitas inserções/remoções em posições variadas |

---
### **Métodos comuns**

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

---
### **Diferenças específicas**

| **Operação**                   | **ArrayList**      | **LinkedList**                      |
| ------------------------------ | ------------------ | ----------------------------------- |
| `removeFirst()` `removeLast()` | **Não disponível** | Sim, métodos específicos para isso  |
| `addFirst(e)` `addLast(e)`     | **Não disponível** | Sim, permite uso como fila ou pilha |











![](attachments/Pasted%20image%2020250815093252.png)