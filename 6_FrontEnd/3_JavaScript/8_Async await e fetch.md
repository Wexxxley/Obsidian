
#Concluded

___
`.then()` e `.catch()` não são a primeira escolha hoje ao lidar com promessas, porque a sintaxe **`async/await` é simplesmente superior** na maioria dos casos. Um dos motivos é que o código com `async/await` é linear e parece síncrono, o que é muito mais fácil para o cérebro humano entender do que os blocos aninhados ou encadeados do `.then()`.
![Pasted image 20250609152634](../../attachments/Pasted%20image%2020250609152634.png)
A função fetch retorna uma promisse por iss precisa do await.

![Pasted image 20250609152931](../../attachments/Pasted%20image%2020250609152931.png)
Essa é a forma antiga com then e catch.
O catch é em caso de erro, e o then é necessário a cada promisse. Nesse caso foram necessários dois, o que torna o código difícil de ler.


**Fetch** é a maneira de fazer requisições de rede.  **Fetch** é **baseada em Promises**, o que a integra perfeitamente com a sintaxe `async/await`.

Ela recebe um argumento principal: a **URL** do recurso que você quer acessar.:
1. A chamada `fetch(url)` retorna imediatamente uma **Promise**.
2. Essa Promise **não resolve com os dados** (JSON, texto, etc.) diretamente. Ela resolve com um objeto chamado **`Response`**.
3. O objeto `Response` é uma representação da resposta HTTP inteira, incluindo o status, cabeçalhos e o corpo da resposta.

Para extrair os dados do corpo da resposta, você precisa usar um método específico do objeto:
- `response.json()`: para transformar o corpo da resposta em um objeto JSON.
- `response.text()`: para obter o corpo como texto puro.
- `response.blob()`: para dados binários (como imagens).

Esses métodos também **retornam uma Promise**, o que significa que temos um processo de duas etapas assíncronas.

---

### Exemplo Prático com `async/await` (A Forma Moderna)

Esta é a maneira mais comum e legível de usar `fetch` hoje.

JavaScript

```
async function buscarUsuarios() {
  const url = 'https://jsonplaceholder.typicode.com/users';

  try {
    // 1. Espera a requisição de rede ser completada e retorna o objeto Response
    const response = await fetch(url);

    // Verificando se a requisição foi bem-sucedida (status 200-299)
    if (!response.ok) {
      throw new Error(`Erro na requisição: ${response.status}`);
    }

    // 2. Espera a transformação do corpo da resposta em JSON
    const data = await response.json();

    // 3. Agora você tem os dados e pode usá-los!
    console.log('Usuários encontrados:', data);
    data.forEach(user => {
      console.log(`- ${user.name}`);
    });

  } catch (error) {
    // Captura erros de rede (ex: sem internet) ou o erro que jogamos acima
    console.error('Falhou a busca por usuários:', error);
  }
}

buscarUsuarios();
```

### Exemplo com `.then()` (A Forma Clássica)

Para entender a base de Promises, veja como o mesmo código funciona com `.then()`:

JavaScript

```
const url = 'https://jsonplaceholder.typicode.com/users';

fetch(url)
  .then(response => {
    // O primeiro .then recebe o objeto Response
    if (!response.ok) {
      throw new Error(`Erro na requisição: ${response.status}`);
    }
    // Retornamos a próxima Promise para o próximo .then
    return response.json(); 
  })
  .then(data => {
    // O segundo .then recebe os dados do .json()
    console.log('Usuários encontrados:', data);
    data.forEach(user => {
      console.log(`- ${user.name}`);
    });
  })
  .catch(error => {
    // .catch captura qualquer erro na cadeia de Promises
    console.error('Falhou a busca por usuários:', error);
  });
```

---

### Indo Além: Enviando Dados (Requisições `POST`)

Para enviar dados, você passa um segundo argumento para a `fetch`: um objeto de configuração.

JavaScript

```
async function criarPost() {
  const url = 'https://jsonplaceholder.typicode.com/posts';

  const novoPost = {
    title: 'Meu Novo Post',
    body: 'Este é o conteúdo do post.',
    userId: 1,
  };

  try {
    const response = await fetch(url, {
      method: 'POST', // Define o método HTTP
      headers: {
        'Content-Type': 'application/json', // Informa ao servidor que estamos enviando JSON
      },
      body: JSON.stringify(novoPost), // O corpo da requisição precisa ser uma string
    });

    if (!response.ok) {
      throw new Error(`Erro: ${response.status}`);
    }

    const data = await response.json();
    console.log('Post criado com sucesso:', data);

  } catch (error) {
    console.error('Falha ao criar o post:', error);
  }
}

criarPost();
```

### Ponto Crucial sobre Erros

Um erro comum é achar que a `fetch` falha (rejeita a Promise) se o status for um erro HTTP como 404 (Não Encontrado) ou 500 (Erro de Servidor).

**Isso não é verdade!**

A Promise da `fetch` só é rejeitada se houver um **erro de rede** (ex: o usuário está sem internet, o servidor não existe). Se o servidor responder com um status de erro (404, 500, etc.), a `fetch` considera a requisição um **sucesso** do ponto de vista da rede.

Por isso é **essencial** verificar `response.ok` (que é `true` para status 200-299) e tratar o erro manualmente, como mostrado nos exemplos.

### Resumo Final

|Característica|Descrição|
|---|---|
|**O que é?**|API moderna para fazer requisições de rede em JavaScript.|
|**Retorna o quê?**|Uma **Promise** que resolve com um objeto **`Response`**.|
|**Como pegar dados?**|Usando métodos como `response.json()` ou `response.text()`, que também retornam Promises.|
|**Sintaxe principal?**|`async/await` é a forma mais limpa e recomendada de usá-la.|
|**Tratamento de Erros**|A Promise só falha em erros de rede. Erros HTTP (404, 500) devem ser checados manualmente com `response.ok`.|
|**Substitui o quê?**|O antigo e complexo `XMLHttpRequest` (XHR).|