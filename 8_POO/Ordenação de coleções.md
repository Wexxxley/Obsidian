
---

### **1. Ordenação de Arrays de Tipos Primitivos**

É necessário o `import java.util.Arrays;`
![400](../attachments/Pasted%20image%2020250816075536.png)

---
### **2. Ordenação de Arrays de Objetos**
Vamos supor que queremos ordenar um array de clientes.
![300](../attachments/Pasted%20image%2020250816081724.png)
Para ordenar os objetos, é precisa saber por qual critério organizar os elementos. Você pode fazer isso de duas maneiras:

#### **2.1 sando a interface `Comparable`**
A sua classe de objeto pode implementar a interface `Comparable` para definir uma "ordem". Com essa interface, é preciso definir uma implementação para ``compareTo``.

O método `compareTo` deve retornar um valor que obedece a três regras simples:
1. **Valor negativo :** Retorne um valor negativo se o objeto atual (`this`) for menor que o `outro`. 
2. **Zero:** Retorne zero se o objeto atual (`this`) for igual a o `outro`.
3. **Valor positivo :** Retorne um valor positivo se o objeto atual (`this`) for maior que o `outro`. 

![500](../attachments/Pasted%20image%2020250816081336.png)
Agora é so usar o sort padrao.
#### **2.2 Usando `Comparator`**
O `Comparator` é ideal para definir regras de ordenação externas à classe do objeto. Ele oferece muito mais flexibilidade, pois permite que você tenha diferentes critérios de ordenação sem precisar modificar a classe original.

![550](../attachments/Pasted%20image%2020250816082838.png)

A forma mais moderna e limpa de usar um `Comparator` é com uma expressão lambda:
![550](../attachments/Pasted%20image%2020250816082904.png)

---
### **3. Ordenando list com tipos primitivos**
É preciso do`` import java.util.Collections;``
![](../attachments/Pasted%20image%2020250816083907.png)

