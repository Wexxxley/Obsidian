
#Concluded

___
### **1. Async a await**
`.then()` e `.catch()` não são a primeira escolha hoje ao lidar com promessas, porque a sintaxe **`async/await` é simplesmente superior** na maioria dos casos. Um dos motivos é que o código com `async/await` é linear e parece síncrono, o que é muito mais fácil para o cérebro humano entender do que os blocos aninhados ou encadeados do `.then()`.
![600](../../attachments/Pasted%20image%2020250609152634.png)

---
### **2. Fetch**
**Fetch** é a maneira de fazer requisições de rede.  **Fetch** é **baseada em Promises**.

Ela recebe a **URL** do recurso que você quer acessar.
1. A chamada `fetch(url)` retorna uma **Promise**.
2. Essa Promise **não se resolve com os dados** diretamente. Ela se resolve com um objeto chamado **`Response`**.
3. `Response` é uma representação da resposta HTTP, incluindo o status, cabeçalhos e o corpo.

Para extrair os dados do corpo, você precisa usar um método específico:
- `response.json()`: para transformar o corpo da resposta em um objeto JSON.
- `response.text()`: para obter o corpo como texto puro.
- `response.blob()`: para dados binários (como imagens).

Esses métodos também **retornam uma Promise**, o que significa que temos um processo de duas etapas assíncronas.

#### **2.1 Recenbendo dados com fetch**
![](../../attachments/Pasted%20image%2020250705144143.png)

#### **2.1 Enviandi dados com fetch**
Para enviar dados, você passa um segundo argumento para a `fetch`: um objeto de configuração.

JavaScript

```

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