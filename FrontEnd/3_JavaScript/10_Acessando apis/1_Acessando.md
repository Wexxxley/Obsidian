

---
![[Pasted image 20250624073206.png]]
![[Pasted image 20250624073222.png]]
1. **`fetch`**:
    - `fetch()`: Faz uma requisições web e retorna uma `Promise`.
    - `await`: Pausa a execução da função até que a `Promise` retornada por `fetch()` seja resolvida.
2. **`response.json();`**:
    - `response.json()`: O objeto `response` retornado não contém diretamente os dados JSON. Ele é um objeto `Response`. O método `.json()` lê o corpo da resposta e o converte em json.
    - `await`: Novamente, pausa a execução até que o corpo JSON seja totalmente lido e parseado. O resultado (a lista de usuários, por exemplo) é armazenado na variável `users`.
3. **`const usersList = document.getElementById('users-list');`**:
    
    - `document.getElementById('users-list')`: Este é um método do DOM (Document Object Model) que permite obter uma referência a um elemento HTML na página usando seu atributo `id`. Neste caso, ele busca o elemento `<ul>` que tem `id="users-list"`. A referência a este elemento é armazenada na variável `usersList`.
4. **`for(const user of users){ ... }`**:
    
    - Este é um loop `for...of` que itera sobre cada item (que representa um usuário) no array `users` (que foi obtido da API).
    - Em cada iteração, a variável `user` conterá um objeto JavaScript com as propriedades de um usuário (por exemplo, `{ id: 1, username: "admin" }`).
5. **`const listItem = document.createElement('li');`**:
    
    - `document.createElement('li')`: Dentro do loop, para cada usuário, um novo elemento HTML `<li>` (item de lista) é criado na memória. Ele ainda não está visível na página.
6. **`listItem.textContent =`Id: ${user.id}; Username: ${user.username};`;`**:
    
    - `listItem.textContent`: Define o conteúdo de texto do elemento `<li>` que acabou de ser criado.
    - `` `Id: ${user.id}; Username: ${user.username};` ``: Isso é um _template literal_ (string com crases). Ele permite incorporar variáveis JavaScript diretamente em uma string. Aqui, ele acessa as propriedades `id` e `username` do objeto `user` e as insere na string.
7. **`usersList.appendChild(listItem);`**:
    
    - `usersList.appendChild(listItem)`: Este método do DOM adiciona o `listItem` (o elemento `<li>` recém-criado e populado com o texto do usuário) como um **filho** do elemento `usersList` (que é o `<ul>`). Isso faz com que o `<li>` apareça na página web, dentro da lista.
8. **Tratamento de Erros no `catch`**:
    
    - `document.getElementById('users-list').innerHTML =`&lt;li>Erro ao carregar usuários&lt;/li>`;`: Se ocorrer qualquer erro dentro do `try` (rede, API, JSON inválido), este código é executado. Ele limpa o conteúdo da lista `<ul>` e insere um único item de lista que exibe a mensagem "Erro ao carregar usuários".
    - `console.log(error);`: Imprime o objeto de erro no console do navegador (geralmente acessível via F12 ou "Inspecionar Elemento" -> "Console"). Isso é crucial para depuração, pois mostra detalhes sobre o que deu errado.
