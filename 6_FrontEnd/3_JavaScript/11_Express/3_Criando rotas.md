#Concluded 

---

É preciso fazer as impotações com o require.

![](../../../attachments/Pasted%20image%2020250706091814.png)

1. **`(request, response)`**: São os dois objetos principais de uma rota no Express.
    - `request`: Contém informações sobre a **requisição** (parâmetros, body, cabeçalhos).
    - `response`: É o objeto usado para **construir e enviar a resposta de volta**.
2. **`response.status(200).json(...)`**: Envia a resposta HTTP. É um encadeamento de métodos:
    - `.status(200)`: Define o código de status da resposta.
    - `.json(...)`: Converte o objeto em uma string JSON. ``resposnse.json()`` é **terminal**.  Uma vez que o método é chamado, o Express considera o trabalho concluído.
3. **`request.params.index`**: Acessa os **parâmetros da rota** definidos na URL. Express extrai o valor que veio no lugar de `:index` e o disponibiliza em `request.params`. como uma string.
4. **`request.params` vs `request.body`**
    - Os parâmetros que vêm da URL são **sempre strings**. 
    - O `request.body` já vem com os dados convetidos. 

![](../../../attachments/Pasted%20image%2020250706090950.png)

