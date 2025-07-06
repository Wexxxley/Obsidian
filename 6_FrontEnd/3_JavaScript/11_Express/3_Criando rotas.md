

---
É preciso fazer as impotações com o require.
![](../../../attachments/Pasted%20image%2020250706084655.png)
1. **`(request, response)`**: São os dois objetos principais de uma rota no Express.
    - `request`: Contém informações sobre a **requisição** (parâmetros, body, cabeçalhos).
    - `response`: É o objeto usado para **construir e enviar a resposta de volta**.
2. **`response.status(200).json(...)`**: Envia a resposta HTTP. É um encadeamento de métodos:
    - `.status(200)`: Define o código de status da resposta.
    - `.json(...)`: Converte o objeto em uma string JSON. ``resposnse.json()`` é **terminal**. Eles finalizam o ciclo de requisição-resposta, enviando a resposta para o cliente. Uma vez que um desses métodos é chamado, o Express considera o trabalho daquela rota concluído.
3. **`request.body`**: Acessa os dados enviados no **corpo (body)** de uma requisição `POST` ou `PUT`. Para que isso funcione, você precisa usar um middleware na sua aplicação principal, como `app.use(express.json());`, que pega o JSON bruto da requisição e o transforma em um objeto JavaScript.
4. **`request.params.index`**: Acessa os **parâmetros da rota** definidos na URL. No caminho `/atualizar/:index`, o Express extrai o valor que veio no lugar de `:index` e o disponibiliza em `request.params`.

A resposta curta é: porque essa é a **última ação da função**.

**Explicação Técnica:**



O `return` em JavaScript serve para duas coisas:

1. Retornar um valor de uma função.
    
2. **Encerrar a execução da função imediatamente.**
    

No seu código, quando `response.status(200).json(alunoDeletado);` é a última linha, não há mais nada para executar depois, então o `return` se torna redundante.

**Quando o `return` é OBRIGATÓRIO?**

Ele é crucial quando você precisa parar a execução **antes** do final da função. Veja a sua validação:

JavaScript

```
if (!nome || !curso || !ira) {
    // AQUI O RETURN É ESSENCIAL
    return response.status(400).json({ error: "'nome', 'curso' e 'ira' são obrigatórios." });
}

// Se não houvesse o 'return' acima, este código seria executado mesmo com dados inválidos!
const novoAluno = AlunoService.create(nome, curso, ira); 
response.status(201).json(novoAluno);
```

Neste caso, o `return` garante que, após enviar a resposta de erro 400, a função para e não tenta criar um aluno com dados inválidos.

---

### Por que o índice precisa de `parseInt` e o `body` não?

Isso se deve à natureza de como os dados são recebidos e processados pelo Express.

1. **`request.params` (Parâmetros da URL):**
    
    - Os parâmetros que vêm da URL (ex: `/deletar/2`) são **sempre strings**. A URL inteira é uma string, e o Express simplesmente extrai a parte correspondente.
        
    - O JavaScript trata índices de array como números. Para usar o valor "2" da URL como um índice de array, você **precisa convertê-lo de string para número**. É para isso que serve o `parseInt()`. Sem ele, você estaria tentando usar uma string para acessar uma posição de array, o que pode levar a comportamentos inesperados.
        
2. **`request.body` (Corpo da Requisição):**
    
    - O `request.body` é populado por um **middleware**, geralmente `express.json()`.
        
    - Este middleware é inteligente. Ele lê a string JSON que o cliente enviou (ex: `{"nome": "Wesley", "curso": "ADS", "ira": 9.5}`) e a **converte em um objeto JavaScript, preservando os tipos de dados originais do JSON**.
        
    - No JSON, `9.5` é um tipo `number`. Portanto, quando o middleware faz o parsing, `request.body.ira` já será um número no seu código. Você não precisa convertê-lo. O mesmo vale para strings, booleanos, arrays e objetos aninhados.
        

**Em resumo:**

- **URL (`params`)**: Sempre string, precisa de conversão manual (`parseInt`) se for usar como número.
    
- **Corpo (`body`)**: Processado por um middleware (`express.json()`) que já converte os dados para os tipos corretos do JavaScript.