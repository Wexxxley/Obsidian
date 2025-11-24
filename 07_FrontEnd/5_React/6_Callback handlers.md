

---
### **1. Callback Handlers**

O fluxo de dados no React é unidirecional (pai para filho via props). Para que um filho comunique uma mudança para o pai (Search informar o App sobre o termo pesquisado), utiliza-se o padrão de **Callback Handler**.

1. O componente Pai (App) define uma função de callback (handleSearch).
2. O Pai passa essa função como prop para o Filho (Search).
3. O Filho executa essa função prop quando o evento ocorre.

**Implementação no Pai (App):**
![](../../attachments/Pasted%20image%2020251124093326.png)

**Implementação no Filho (Search):**
![](../../attachments/Pasted%20image%2020251124093340.png)

    
2. **Passagem por Referência:** Quando o `App` faz isso:
```jsx
<Search onSearch={handleSearch} />
```

Ele está pegando a **referência** da função handleSearch e entregando para o componente Search dentro de uma variável chamada onSearch.
    
3. **Execução (No Filho - `Search`):** Dentro do `Search`, quando o usuário digita, a função `handleChange` é acionada.
```jsx
const handleChange = (event) => {
   // ...
   props.onSearch(event); // AQUI ESTÁ O SEGREDO
};
```
    
Quando `Search` executa `props.onSearch()`, ele está efetivamente executando a função `handleSearch` que pertence ao `App`, **mas disparando-a de dentro do `Search`**.





















### Rastreamento da Execução (Trace)

Vamos seguir o caminho do código quando você digita a letra **"A"**:

1. **Navegador:** Detecta o evento de digitação no `<input>` dentro do componente `Search`.
    
2. **Search (handleChange):** O React dispara a função local `handleChange` dentro do `Search`.
    
3. **Search (Chamada da Prop):** A linha `props.onSearch(event)` é executada.
    
    - O `Search` não sabe o que essa função faz. Ele apenas executa a função que recebeu.
        
4. **Salto de Escopo:** Como `props.onSearch` é uma referência para `handleSearch` do `App`, a execução do código "salta" para o arquivo `App.jsx`.
    
5. **App (handleSearch):** A função `handleSearch` do Pai é executada, recebendo o `event` que veio lá do filho.
    
6. **Console:** O `console.log` imprime "A".
    

### Resumo Técnico

O "Callback Handler" é simplesmente o Pai emprestando uma função sua para o Filho. O Filho usa essa função emprestada para enviar dados de volta (através dos argumentos da função), permitindo que o Pai saiba o que aconteceu no Filho.


![](../../attachments/Pasted%20image%2020251124065353.png)