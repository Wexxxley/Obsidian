
---

### **1. Ordenação de Arrays de Tipos Primitivos**

É necessário o `import java.util.Arrays;`
![400](attachments/Pasted%20image%2020250816075536.png)
---
### **2. Ordenação de Arrays de Objetos**
Vamos supor que queremos ordenar um array de clientes.
![300](attachments/Pasted%20image%2020250816075750.png)

Para ordenar os objetos, é precisa saber por qual critério organizar os elementos. Você pode fazer isso de duas maneiras:

#### **2.1 sando a interface `Comparable`**
A sua classe de objeto pode implementar a interface `Comparable` para definir uma "ordem". Com essa interface, é preciso definir uma implementação para ``compareTo``.

O método `compareTo` deve retornar um valor que obedece a três regras simples:
1. **Valor negativo :** Retorne um valor negativo se o objeto atual (`this`) for menor que o `outro`. 
2. **Zero:** Retorne zero se o objeto atual (`this`) for igual a o `outro`.
3. **Valor positivo :** Retorne um valor positivo se o objeto atual (`this`) for maior que o `outro`. 

![](attachments/Pasted%20image%2020250816081240.png)
#### b) Usando a interface `Comparator`

Se você precisa ordenar por critérios diferentes (como por nome e não por preço), ou se não pode modificar a classe do objeto, você pode passar um `Comparator` como argumento para o `Arrays.sort()`.

Java

```
import java.util.Arrays;
import java.util.Comparator;

public class ExemploOrdenacaoComComparator {
    public static void main(String[] args) {
        Produto[] produtos = {
            new Produto("Fone", 150.0),
            new Produto("Celular", 2500.0),
            new Produto("Mouse", 80.0)
        };
        
        // Ordena por nome (critério alternativo) usando um Comparator
        Arrays.sort(produtos, new Comparator<Produto>() {
            @Override
            public int compare(Produto p1, Produto p2) {
                return p1.getNome().compareTo(p2.getNome());
            }
        });
        
        for (Produto p : produtos) {
            System.out.println(p);
        }
    }
}
```

**Saída:**

```
Produto{nome='Celular', preco=2500.0}
Produto{nome='Fone', preco=150.0}
Produto{nome='Mouse', preco=80.0}
```

A forma mais moderna e limpa de usar um `Comparator` é com uma **expressão lambda**:

Java

```
// Ordena por nome com lambda
Arrays.sort(produtos, (p1, p2) -> p1.getNome().compareTo(p2.getNome()));
```