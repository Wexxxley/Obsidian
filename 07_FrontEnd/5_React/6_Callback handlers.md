
#Concluded 

---
### **1. Callback Handlers**

O fluxo de dados no React é unidirecional (pai para filho via props). Para que um filho comunique uma mudança para o pai (Search informar o App sobre o termo pesquisado), utiliza-se o padrão de **Callback Handler**.

1. O componente Pai define uma função de callback.
2. O Pai passa essa função como prop para o Filho.
3. O Filho executa essa função prop quando o evento ocorre.

**Implementação no Pai (App):**
![](../../attachments/Pasted%20image%2020251124093326.png)
Quando o `App` faz isso: `<Search onSearch={handleSearch}/>` Ele está pegando a **referência** da função handleSearch e entregando para o componente dentro de uma variável chamada onSearch.

**Implementação no Filho (Search):**
![](../../attachments/Pasted%20image%2020251124093340.png)
Dentro do `Search`, quando o usuário digita, a função `handleChange` é acionada. Quando `Search` executa `props.onSearch()`, ele está efetivamente executando a função `handleSearch` que pertence ao `App`, mas disparando-a de dentro do `Search`.

---
### **2. Lifting State**

Atualmente, o estado `searchTerm` reside no componente `Search`. No entanto, o componente `List` (que renderiza os dados) é irmão do `Search`. No React, irmãos não compartilham dados diretamente.

Para que o termo de busca afete a lista, precisamos **elevar o estado** para o componente pai comum mais próximo, que é o `App`. O `App` passará o estado para baixo: como _props_ para a `List` e como _callback_ para o `Search` (para atualizar o estado).

1. **Remoção do Estado no Filho:** Removemos o hook `useState` do componente `Search`.
2. **Adição do Estado no Pai:** Adicionamos o hook `useState` no componente `App`.
3. **Filtragem de Dados:** Utilizamos o método `filter()` do JavaScript no `App` para criar uma nova lista derivada antes de passá-la para o componente `List`.

**Código Refatorado (`src/App.jsx`):**
![](../../attachments/Pasted%20image%2020251124101046.png)
![](../../attachments/Pasted%20image%2020251124101113.png)

1. **Input:** O usuário digita no `Search`.    
2. **Propagação:** O evento `onChange` dispara `props.onSearch`, que executa `handleSearch`.
3. **State Update:** `handleSearch` atualiza o estado `searchTerm` no `App` via `setSearchTerm`.
4. **Re-renderização:** O `App` é re-renderizado.
5. **Cálculo Derivado:** Durante a renderização, a constante `searchedStories` é recalculada filtrando o array original `stories` com o novo `searchTerm` .
6. **Atualização de Props:** O componente `List` recebe a nova lista filtrada via prop `list`.

![300](../../attachments/Pasted%20image%2020251124101004.png)

![](../../attachments/Pasted%20image%2020251124134442.png)
A regra é: <mark style="background: #ADCCFFA6;">Gerencie o estado no componente onde todos os componentes dependentes desse estado possam acessá-lo.</mark>
