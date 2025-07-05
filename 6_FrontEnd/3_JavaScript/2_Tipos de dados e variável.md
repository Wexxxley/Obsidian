
Status: #Concluded 

---
### **1. Tipos primitivos**

1. **String**:
    ```js
    let nome = "Maria";
    ```
2. **Number** – Representa todos os números, seja inteiro, negativo, fllutuante.
    ```js
    let idade = 30;
    let altura = 1.75;
    let vontadeDeViver = -1000;
    ```
3. **Boolean** – Verdadeiro ou falso:
    ```js
    let ativo = true;
    ```
4. **Null** – Valor nulo intencional:
    ```js
    let dados = null;
    ```

> [!NOTE]
> JavaScript é **dinamicamente tipado**: o tipo é definido automaticamente em tempo de execução e pode mudar.

---
### **2. Tipos de referência**

1. **Object** – Estrutura chave-valor:
    ```js
    let pessoa = { nome: "João", idade: 25 };
    ```
2. **Array** – Lista de valores:
    ```js
    let frutas = ["maçã", "banana", "laranja"];
    ```
3. **Function** – Bloco de código reutilizável:
    ```js
    function saudacao() {
      console.log("Olá!");
    }
    ```
---
### **3. Conversão de tipos**

**Conversão explícita**
```js
Number("123")        // 123
parseInt("123abc")   // 123
parseFloat("3.14")   // 3.14

String(123)          // "123"
(123).toString()     // "123"
```

---
### **4. Comparação de objetos**
No js temos `==` e `===`. O primeiro compara o valor em si, mas o js faz muitas converções por baixo dos panos, então não é confiável. Já o  `===` compara dois valores e só retorna true se forem exatamente iguais. 
```js
5 == '5'     // true   → converte string para número
5 === '5'    // false  → número ≠ string

true == 1    // true   → true vira 1
true === 1   // false  → boolean ≠ número

null == undefined   // true
null === undefined  // false
```

---
### **5. Variável e constante**
``let`` define uma variável que pode sofrer alteração. ``const`` cria uma constante, ou seja, o valor não pode ser alterado em tempo de execução.
![Pasted image 20250505142357](../../attachments/Pasted%20image%2020250505142357.png)
Note que foi usado crases para permitir a inclusão de variáveis no texto.

![Pasted image 20250505155217](../../attachments/Pasted%20image%2020250505155217.png)
O ``prompt`` recebe valores do terminal.


