
#Concluded 

---
### **1. Get all**
![Pasted image 20250624073206](../../../attachments/Pasted%20image%2020250624073206.png)
![Pasted image 20250624073222](../../../attachments/Pasted%20image%2020250624073222.png)
1. **`fetch`**: Faz uma requisições web e retorna uma `Promise`.
2. **`response.json()`**: O objeto `response` retornado não contém diretamente os dados JSON. O método `.json()` lê o body da resposta e o converte em json.
3. **`document.createElement('li');`**: Um novo elemento HTML `<li>` é criado na memória. 
4. **`listItem.textContent`**: Define o conteúdo de texto do elemento. Com esse atributo somente texto literal é colocado. Diferente do innerHtml que pode criar tags. 
5. **`usersList.appendChild(listItem)`**: Adiciona o `listItem` como um **filho** de `usersList`.
---
### **2. Criar recurso com formulário (API espera um JSON)**
![Pasted image 20250624074302](../../../attachments/Pasted%20image%2020250624074302.png)
![Pasted image 20250624074321](../../../attachments/Pasted%20image%2020250624074321.png)
1. **`addEventListener('submit', async function(e) {...})`**: Adiciona um ouvinte para o evento de envio do formulário.`async`Torna a função assíncrona, permitindo o uso de `await` dentro dela.
2. `fetch()`: Envia uma requisição HTTP do tipo POST
3. `method: 'POST'`: Define o método HTTP como POST.
4. `headers:{'Content-Type':'application/json'}`: Informa que os dados estão em JSON.
5. `body: JSON.stringify({ username, password })`: Converte para uma string JSON.

---
### **3. Get por id**
![Pasted image 20250624080148](../../../attachments/Pasted%20image%2020250624080148.png)
![Pasted image 20250624080206](../../../attachments/Pasted%20image%2020250624080206.png)

---
### **4. Delete**
![Pasted image 20250624081735](../../../attachments/Pasted%20image%2020250624081735.png)
![Pasted image 20250624081804](../../../attachments/Pasted%20image%2020250624081804.png)

