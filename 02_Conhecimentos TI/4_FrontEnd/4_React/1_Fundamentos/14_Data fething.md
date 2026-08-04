

---
O objetivo técnico é consumir dados reais de uma API remota. Para isso, utilizaremos o endpoint de busca da API do Hacker News.

![](../../../../attachments/Pasted%20image%2020251125145434.png)
![](../../../../attachments/Pasted%20image%2020251125150222.png)
1. **`fetch(url)`**: Inicia uma requisição de rede. Retorna uma Promise.
    
2. **`.then(response => response.json())`**: O `fetch` não retorna os dados JSON diretamente. Ele retorna um objeto de resposta HTTP. 
    
3. **Mapeamento de Dados (`result.hits`)**: A estrutura de dados retornada pela API do Hacker News é um objeto que contém uma lista de histórias na propriedade `hits`. Portanto, atualizamos o estado com `result.hits`
    
4. **Busca Server-Side:** Observe que removemos a variável `searchedStories` (filtro no cliente). Agora, passamos o `searchTerm` diretamente na URL da API. Isso significa que a filtragem está sendo feita pelo servidor do Hacker News, não mais pelo navegador.
    
5. **Dependência do `useEffect`**: Adicionamos `[searchTerm]` ao array de dependências. Isso faz com que, a cada letra que você digita, o React execute o efeito novamente e faça uma nova requisição para a API (Server-side Search).

No estado atual, a aplicação faz uma requisição a cada tecla pressionada. Isso é ineficiente e pode causar erros de limite de taxa da API.