

---
Para controlar o envio de dados, utilizamos o elemento nativo `<form>`. Ele oferece dois benefícios automáticos:
1. **Submit via Enter**
2. **Submit via Botão:** Qualquer botão com `type="submit"` dentro do form dispara o envio.

#### 1. O Evento `onSubmit` e `preventDefault`

Em HTML puro, ao submeter um formulário, o navegador recarrega a página inteira. Em uma SPA (Single-Page Application) com React, **não queremos que a página recarregue**.

Para evitar isso, utilizamos o método `event.preventDefault()` dentro do manipulador de evento do formulário .

#### 2. Extraindo o Componente `SearchForm`

Para manter o código organizado, o livro sugere extrair a parte visual do formulário para um componente dedicado `SearchForm`.

### Implementação Técnica (`src/App.jsx`)

Faremos três mudanças principais:

1. Criar o componente `SearchForm`.
    
2. Alterar a lógica de busca no `App` para usar um estado de `url` (que só muda no submit) em vez de depender diretamente do `searchTerm`.
    
3. Atualizar o `useEffect` para depender dessa `url` e não mais do termo de busca digitado.
    

JavaScript

```
import * as React from 'react';

const API_ENDPOINT = 'https://hn.algolia.com/api/v1/search?query=';

const useStorageState = (key, initialState) => {
  const [value, setValue] = React.useState(
    localStorage.getItem(key) || initialState
  );

  React.useEffect(() => {
    localStorage.setItem(key, value);
  }, [value, key]);

  return [value, setValue];
};

const App = () => {
  const [searchTerm, setSearchTerm] = useStorageState('search', 'React');
  
  // 1. Novo Estado: URL confirmada para busca
  // Inicializa com a busca padrão ('React')
  const [url, setUrl] = React.useState(
    `${API_ENDPOINT}${searchTerm}`
  );

  const [stories, setStories] = React.useState([]);
  const [isLoading, setIsLoading] = React.useState(false);
  const [isError, setIsError] = React.useState(false);

  // 2. O efeito agora depende da 'url', não mais de 'searchTerm' (digitação)
  React.useEffect(() => {
    setIsLoading(true);

    fetch(url) // Usa a URL confirmada
      .then((response) => response.json())
      .then((result) => {
        setStories(result.hits);
        setIsLoading(false);
      })
      .catch(() => {
        setIsError(true);
        setIsLoading(false);
      });
  }, [url]); // Só roda se a URL mudar (no submit)

  const handleRemoveStory = (item) => {
    const newStories = stories.filter(
      (story) => story.objectID !== item.objectID
    );
    setStories(newStories);
  };

  // Atualiza apenas o input visualmente, sem disparar fetch
  const handleSearchInput = (event) => {
    setSearchTerm(event.target.value);
  };

  // 3. Handler de Submissão do Formulário
  const handleSearchSubmit = (event) => {
    // Define a nova URL para disparar o useEffect
    setUrl(`${API_ENDPOINT}${searchTerm}`);
    
    // Previne o recarregamento da página (comportamento padrão do HTML)
    event.preventDefault();
  };

  return (
    <div>
      <h1>My Hacker Stories</h1>

      {/* 4. Uso do Componente de Formulário */}
      <SearchForm
        searchTerm={searchTerm}
        onSearchInput={handleSearchInput}
        onSearchSubmit={handleSearchSubmit}
      />

      <hr />

      {isError && <p>Something went wrong ...</p>}

      {isLoading ? (
        <p>Loading ...</p>
      ) : (
        <List list={stories} onRemoveItem={handleRemoveStory} />
      )}
    </div>
  );
};

// 5. Componente SearchForm Extraído
const SearchForm = ({ searchTerm, onSearchInput, onSearchSubmit }) => (
  <form onSubmit={onSearchSubmit}>
    <InputWithLabel
      id="search"
      value={searchTerm}
      onInputChange={onSearchInput}
    >
      <strong>Search:</strong>
    </InputWithLabel>

    {/* Botão de submit desabilitado se o campo estiver vazio */}
    <button type="submit" disabled={!searchTerm}>
      Submit
    </button>
  </form>
);

const InputWithLabel = ({ id, value, type = 'text', onInputChange, children }) => (
  <>
    <label htmlFor={id}>{children}</label>
    &nbsp;
    <input
      id={id}
      type={type}
      value={value}
      onChange={onInputChange}
    />
  </>
);

const List = ({ list, onRemoveItem }) => (
  <ul>
    {list.map((item) => (
      <Item key={item.objectID} item={item} onRemoveItem={onRemoveItem} />
    ))}
  </ul>
);

const Item = ({ item, onRemoveItem }) => (
  <li>
    <span>
      <a href={item.url}>{item.title}</a>
    </span>
    <span>{item.author}</span>
    <span>{item.num_comments}</span>
    <span>{item.points}</span>
    <span>
      <button type="button" onClick={() => onRemoveItem(item)}>
        Dismiss
      </button>
    </span>
  </li>
);

export default App;
```

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
