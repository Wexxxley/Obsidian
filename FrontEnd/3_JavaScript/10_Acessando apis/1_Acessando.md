

---
### **1. Get all**
![[Pasted image 20250624073206.png]]
![[Pasted image 20250624073222.png]]
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

![[Pasted image 20250624074302.png]]
![[Pasted image 20250624074321.png]]
### JavaScript: Enviando dados com `fetch`

js

CopiarEditar

`document.getElementById('user-form').addEventListener('submit', async function(e) {     e.preventDefault(); // Evita que o formulário recarregue a página`

- Intercepta o envio do formulário com um **listener de evento `submit`**.
    
- `e.preventDefault()` cancela o comportamento padrão (recarregar a página).
    

---

### 🔹 Capturando dados do formulário

js

CopiarEditar

    `const username = document.getElementById('username').value;     const password = document.getElementById('password').value;`

- Obtém os valores digitados nos campos de entrada.
    

---

### 🔹 Enviando para a API com `fetch`

js

CopiarEditar

    `const response = await fetch('http://127.0.0.1:8000/users/create', {         method: 'POST',         headers: { 'Content-Type': 'application/json' },         body: JSON.stringify({ username, password })     });`

- Faz uma requisição **POST** para `http://127.0.0.1:8000/users/create` (possivelmente um endpoint FastAPI).
    
- Envia os dados como **JSON** no corpo da requisição.
    
- `headers` define que o tipo dos dados enviados é JSON.
    
- `JSON.stringify({ username, password })`: transforma os dados em texto JSON.
    

---

### 🔹 Tratando a resposta da API

js

CopiarEditar

    `const data = await response.json();     if (response.ok) {         document.getElementById('user-create-result').textContent = 'Usuário criado com sucesso!';     } else {         document.getElementById('user-create-result').textContent = data.detail || 'Erro ao criar usuário';     }`

- `await response.json()`: extrai os dados da resposta em formato JSON.
    
- `response.ok`: verifica se a resposta tem status HTTP entre 200 e 299.
    
- Se deu tudo certo, mostra uma mensagem de sucesso no elemento `user-create-result`.
    
- Se deu erro, mostra a mensagem vinda do backend (`data.detail`) ou uma mensagem genérica.
    

---

### 🔹 Tratando erro de conexão (API offline, etc)

js

CopiarEditar

`} catch (err) {     document.getElementById('user-create-result').textContent = 'Erro de conexão com a API'; }`

- Se a requisição falhar (ex: API fora do ar), mostra uma mensagem apropriada.