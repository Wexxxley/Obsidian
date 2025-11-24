


---
### **1. Callback Handlers**

O fluxo de dados no React é unidirecional (pai para filho via props). Para que um filho comunique uma mudança para o pai (Search informar o App sobre o termo pesquisado), utiliza-se o padrão de **Callback Handler**.

1. O componente Pai (App) define uma função de callback (handleSearch).
2. O Pai passa essa função como prop para o Filho (Search).
3. O Filho executa essa função prop quando o evento ocorre.

**Implementação no Pai (App):**
![](../../attachments/Pasted%20image%2020251124093326.png)
Quando o `App` faz isso: `<Search onSearch={handleSearch}/>` Ele está pegando a **referência** da função handleSearch e entregando para o componente Search dentro de uma variável chamada onSearch.

**Implementação no Filho (Search):**
![](../../attachments/Pasted%20image%2020251124093340.png)
Dentro do `Search`, quando o usuário digita, a função `handleChange` é acionada. Quando `Search` executa `props.onSearch()`, ele está efetivamente executando a função `handleSearch` que pertence ao `App`, mas disparando-a de dentro do `Search`.


---
### **2. Lifting State**

Atualmente, o estado `searchTerm` reside no componente `Search`. No entanto, o componente `List` (que renderiza os dados) é irmão do `Search`. No React, irmãos não compartilham dados diretamente.

Para que o termo de busca afete a lista, precisamos **elevar o estado** para o componente pai comum mais próximo, que é o `App`. O `App` passará o estado para baixo: como _props_ para a `List` (os dados filtrados) e como _callback_ para o `Search` (para atualizar o estado).

**Implementação Técnica:**

1. **Remoção do Estado no Filho:** Removemos o hook `useState` do componente `Search`.
2. **Adição do Estado no Pai:** Adicionamos o hook `useState` no componente `App`.
3. **Filtragem de Dados:** Utilizamos o método `filter()` do JavaScript no `App` para criar uma nova lista derivada antes de passá-la para o componente `List`.

**Código Refatorado (`src/App.jsx`):**

JavaScript

```jsx
import * as React from 'react';

const App = () => {
  const stories = [
    {
      title: 'React',
      url: 'https://react.dev/',
      author: 'Jordan Walke',
      objectID: 0,
    },
    {
      title: 'Redux',
      url: 'https://redux.js.org/',
      author: 'Dan Abramov, Andrew Clark',
      objectID: 1,
    },
  ];

  // 1. O Estado é instanciado no Pai (Lifting State)
  const [searchTerm, setSearchTerm] = React.useState('');

  // 2. O Callback Handler atualiza o estado no Pai
  const handleSearch = (event) => {
    setSearchTerm(event.target.value);
  };

  // 3. Os dados são filtrados baseados no estado atual antes da renderização
  // O método filter cria um novo array contendo apenas os itens que satisfazem a condição
  const searchedStories = stories.filter(function (story) {
    return story.title.toLowerCase().includes(searchTerm.toLowerCase());
  });

  return (
    <div>
      <h1>My Hacker Stories</h1>

      {/* Passamos o callback para permitir que o Search atualize o estado */}
      <Search onSearch={handleSearch} />

      <hr />

      {/* Passamos a lista JÁ FILTRADA para o componente de visualização */}
      <List list={searchedStories} />
    </div>
  );
};

const Search = (props) => {
  // O componente agora é stateless (sem estado interno de busca)
  // Ele apenas repassa o evento para o pai via props
  
  return (
    <div>
      <label htmlFor="search">Search: </label>
      <input id="search" type="text" onChange={props.onSearch} />
    </div>
  );
};

const List = (props) => (
  <ul>
    {props.list.map((item) => (
      <Item key={item.objectID} item={item} />
    ))}
  </ul>
);

const Item = (props) => (
  <li>
    <span>
      <a href={props.item.url}>{props.item.title}</a>
    </span>
    <span>{props.item.author}</span>
    <span>{props.item.num_comments}</span>
    <span>{props.item.points}</span>
  </li>
);

export default App;
```

**Análise do Fluxo de Dados:**

1. **Input:** O usuário digita no `Search`.
    
2. **Propagação:** O evento `onChange` dispara `props.onSearch`, que executa `handleSearch` no `App`.
    
3. **State Update:** `handleSearch` atualiza o estado `searchTerm` no `App` via `setSearchTerm`.
    
4. **Re-renderização:** O `App` é re-renderizado.
    
5. **Cálculo Derivado:** Durante a renderização, a constante `searchedStories` é recalculada filtrando o array original `stories` com o novo `searchTerm` .
    
6. **Atualização de Props:** O componente `List` recebe a nova lista filtrada via prop `list`.
    
7. **DOM Update:** O React atualiza a lista na tela, removendo os itens que não correspondem à busca.
    

A regra técnica fundamental aqui é: **Gerencie o estado no componente onde todos os componentes dependentes desse estado possam acessá-lo (seja para leitura ou escrita)** .

