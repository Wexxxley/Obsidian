
#Concluded 

---
### **1. Get all**
![Pasted image 20250624073206](../../../attachments/Pasted%20image%2020250624073206.png)
![Pasted image 20250624073222](../../../attachments/Pasted%20image%2020250624073222.png)
1. **`fetch`**:
    - `fetch()`: Faz uma requisições web e retorna uma `Promise`.
    - `await`: Pausa a execução da função até que a `Promise` retornada por `fetch()` seja resolvida.
2. **`response.json();`**:
    - `response.json()`: O objeto `response` retornado não contém diretamente os dados JSON. O método `.json()` lê o corpo da resposta e o converte em json.
    - `await`: Novamente, pausa a execução até que o corpo JSON seja totalmente convertido.
3. **`document.createElement('li');`**:
    - `document.createElement('li')`: Dentro do loop, para cada usuário, um novo elemento HTML `<li>` é criado na memória. 
4. **`listItem.textContent = ...`**:
    - `listItem.textContent`: Define o conteúdo de texto do elemento. Com esse atributo somente texto literal é colocado. Diferente do innerHtml que pode criar tags. O que pode causar a introdução de código malicioso.
5. **`usersList.appendChild(listItem);`**:
    - `usersList.appendChild(listItem)`: Este método adiciona o `listItem` como um **filho** do elemento `usersList`.

---
### **2. Criar modelo com formulário (API espera um JSON)**

![Pasted image 20250624074302](../../../attachments/Pasted%20image%2020250624074302.png)
![Pasted image 20250624074321](../../../attachments/Pasted%20image%2020250624074321.png)
1. **`addEventListener('submit', async function(e) {...})`**:
    - `addEventListener('submit', ...)`: Adiciona um ouvinte para o evento de envio do formulário.
    - `async function(e)`: Torna a função assíncrona, permitindo o uso de `await` dentro dela.
    - `e.preventDefault()`: Impede que a página recarregue ao submeter o formulário.
2. **`getElementById('username').value;`** 
    - `document.getElementById(...).value`: Acessa o valor atual digitado nos campos.
3. **`fetch`**:
    - `fetch()`: Envia uma requisição HTTP do tipo POST
    - `method: 'POST'`: Define o método HTTP como POST.
    - `headers: { 'Content-Type': 'application/json' }`: Informa que os dados estão no formato JSON.
    - `body: JSON.stringify({ username, password })`: Converte os dados do formulário para uma string JSON.
4. **`const data = await response.json();`**:    
    - Lê o corpo da resposta e o interpreta como JSON e aguarda a conversão completa do corpo da resposta em objeto JavaScript.
5. **`if (response.ok) { ... } else { ... }`**:
    - `response.ok`: Retorna `true` se o status da resposta HTTP estiver entre 200 e 299, indicando sucesso.
    - Se verdadeiro, exibe a mensagem de sucesso.

---
### **3. Get por id**
![Pasted image 20250624080148](../../../attachments/Pasted%20image%2020250624080148.png)
![Pasted image 20250624080206](../../../attachments/Pasted%20image%2020250624080206.png)

---
### **4. Delete**
![Pasted image 20250624081735](../../../attachments/Pasted%20image%2020250624081735.png)
![Pasted image 20250624081804](../../../attachments/Pasted%20image%2020250624081804.png)

