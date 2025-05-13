Status: #Concluded 

---
### **1. Tipos primitivos**

São imutáveis e armazenam um único valor.
1. **String** – Texto entre aspas:
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
4. **Undefined** – Variável declarada, mas sem valor:
    ```js
    let x; 
    ```
5. **Null** – Valor nulo intencional:
    ```js
    let dados = null;
    ```

> [!NOTE]
> JavaScript é **dinamicamente tipado**: o tipo é definido automaticamente em tempo de execução e pode mudar.

---
### **2. Tipos de referência (objetos)**
São mutáveis e armazenam coleções ou funcionalidades:

1. **Object** – Estrutura com pares chave-valor:
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
4. **Date, Map, Set, etc.** – Objetos especiais do JS.

---
### **3. Conversão de tipos**

#### Conversão implícita
O próprio JavaScript converte o tipo automaticamente quando necessário. JavaScript tenta "adivinhar" o que você quis dizer, o que pode causar confusões.
```js
"5" * 2      // 10  → string "5" é convertida para número
"5" + 2      // "52" → número 2 é convertido para string
true + 1     // 2  → true vira 1
```
#### Conversão explícita
**Para Número**
```js
Number("123")        // 123
parseInt("123abc")   // 123
parseFloat("3.14")   // 3.14
```
**Para string**
```js
String(123)          // "123"
(123).toString()     // "123"
```

---
### **4. Comparação de objetos**
No js temos `==` e `===`. O primeiro compara o valor em si, mas o js faz muitas converções por baixo dos panos, então não é confiável. Já o  `===` compara dois valores e só retorna true se forem exatamente iguais. O **valor e o tipo** precisam ser os mesmos.
```
5 == '5'     // true   → converte string para número
5 === '5'    // false  → número ≠ string

true == 1    // true   → true vira 1
true === 1   // false  → boolean ≠ número

null == undefined   // true
null === undefined  // false
```

---
### 5. Variáveis e impressão
``let`` define uma variável que pode sofrer alteração de valor. ``const`` cria uma constante, ou seja, o valor não pode ser alterado em tempo de execução.
![[Pasted image 20250505142357.png]]
![[Pasted image 20250505155217.png]]
O ``prompt`` recebe valores do user.