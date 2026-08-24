

---
Para controlar o envio de dados, utilizamos o elemento nativo `<form>`. Ele oferece dois benefícios automáticos:

1. **Submit via Enter do input**
2. **Submit via Botão**

---
### 1. O Evento onSubmit e preventDefault

Em HTML puro, ao submeter um formulário, o navegador recarrega a página inteira. Em uma SPA com React, não queremos que a página recarregue.

Para evitar isso, utilizamos o método `event.preventDefault()` dentro do manipulador de evento do formulário .

Para manter o código organizado, é bom extrair a parte visual do formulário para um componente dedicado `SearchForm`.

**Faremos três mudanças principais:**
1. Criar o componente `SearchForm`.
2. Alterar a lógica de busca no `App` para usar um estado de `url` (que só muda no submit) em vez de depender diretamente do `searchTerm`.
3. Atualizar o `useEffect` para depender dessa `url` e não mais do termo de busca digitado.
![](../../../../../attachments/Pasted%20image%2020251125180606.png)
![](../../../../../attachments/Pasted%20image%2020251125180832.png)

![](../../../../../attachments/Pasted%20image%2020251125180547.png)
### Resumo da Lógica

1. O usuário digita → `handleSearchInput` atualiza `searchTerm`. (O input muda, mas nenhuma requisição é feita).
    
2. O usuário clica em "Submit" ou aperta Enter → O `form` dispara `onSubmit`.
    
3. `handleSearchSubmit` é executado:
    
    - Previne o refresh (`preventDefault`).
        
    - Atualiza o estado `url` com o valor atual de `searchTerm`.
        
4. O `useEffect` detecta que `url` mudou e dispara o `fetch`.
    

Isso resolve completamente o problema de performance e cria uma experiência de usuário padrão de formulários web.

---

Isso cobre o essencial dos **Fundamentos**. O próximo passo natural seria **Estilização (CSS)** ou **Deploy**. Como você quer velocidade, sugiro pularmos tópicos avançados e irmos direto para **Styling in React** (Página 159) para deixar isso menos feio, ou para o **Deploy** se preferir. O que acha?
