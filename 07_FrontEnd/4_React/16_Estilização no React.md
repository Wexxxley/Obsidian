

---
No React, a estilização funciona de forma muito similar ao HTML padrão, mas com duas diferenças  que você precisa memorizar:

1. **clas vira className**
2. **Estilos Inline são Objetos:** Ao usar o atributo `style`, você não passa uma string (`"color: red"`), mas sim um objeto JavaScript (`{{ color: 'red' }}`).


### 1. Criando o CSS (`src/App.css`)

Crie (ou edite) o arquivo `src/App.css` na mesma pasta do `App.jsx` e cole o seguinte estilo. Isso vai criar um layout responsivo com gradiente e botões estilizados.

CSS

```
/* src/App.css */

.container {
  height: 100vw;
  padding: 20px;
  background: #83a4d4;
  background: linear-gradient(to left, #b6fbff, #83a4d4); /* Gradiente de fundo */
  color: #171212;
  font-family: sans-serif;
}

.headline-primary {
  font-size: 48px;
  font-weight: 300;
  letter-spacing: 2px;
}

.search-form {
  padding: 10px 0 20px 0;
  display: flex;
  align-items: baseline;
}

.label {
  border-top: 1px solid #171212;
  border-left: 1px solid #171212;
  padding-left: 5px;
  font-size: 24px;
}

.input {
  border: none;
  border-bottom: 1px solid #171212;
  background-color: transparent;
  font-size: 24px;
  margin-left: 5px;
}

.button {
  background: transparent;
  border: 1px solid #171212;
  padding: 5px;
  cursor: pointer;
  transition: all 0.1s ease-in;
  margin-left: 10px;
}

.button:hover {
  background: #171212;
  color: #ffffff;
}

.button_small {
  padding: 5px;
}

.button_large {
  padding: 10px;
}

.item {
  display: flex;
  align-items: center;
  padding-bottom: 5px;
}

/* Seleciona os spans dentro do item para garantir alinhamento */
.item > span {
  padding: 0 5px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.item > span > a {
  color: inherit;
  text-decoration: none;
}
```

### 2. Aplicando as Classes no JSX (`src/App.jsx`)

Agora precisamos:

1. Importar o arquivo CSS no topo.
    
2. Adicionar os `className` nos elementos.
    
3. Adicionar `style` inline para definir a largura das colunas da lista (40%, 30%, etc).
    

Aqui está o código atualizado:

JavaScript

```
import * as React from 'react';
import './App.css'; // <--- 1. Importação do CSS

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
  const [url, setUrl] = React.useState(`${API_ENDPOINT}${searchTerm}`);
  const [stories, setStories] = React.useState([]);
  const [isLoading, setIsLoading] = React.useState(false);
  const [isError, setIsError] = React.useState(false);

  React.useEffect(() => {
    setIsLoading(true);

    fetch(url)
      .then((response) => response.json())
      .then((result) => {
        setStories(result.hits);
        setIsLoading(false);
      })
      .catch(() => {
        setIsError(true);
        setIsLoading(false);
      });
  }, [url]);

  const handleRemoveStory = (item) => {
    const newStories = stories.filter(
      (story) => story.objectID !== item.objectID
    );
    setStories(newStories);
  };

  const handleSearchInput = (event) => {
    setSearchTerm(event.target.value);
  };

  const handleSearchSubmit = (event) => {
    setUrl(`${API_ENDPOINT}${searchTerm}`);
    event.preventDefault();
  };

  return (
    // Adicionado className "container"
    <div className="container">
      {/* Adicionado className "headline-primary" */}
      <h1 className="headline-primary">My Hacker Stories</h1>

      <SearchForm
        searchTerm={searchTerm}
        onSearchInput={handleSearchInput}
        onSearchSubmit={handleSearchSubmit}
      />

      {isError && <p>Something went wrong ...</p>}

      {isLoading ? (
        <p>Loading ...</p>
      ) : (
        <List list={stories} onRemoveItem={handleRemoveStory} />
      )}
    </div>
  );
};

const SearchForm = ({ searchTerm, onSearchInput, onSearchSubmit }) => (
  // Adicionado className "search-form"
  <form onSubmit={onSearchSubmit} className="search-form">
    <InputWithLabel
      id="search"
      value={searchTerm}
      onInputChange={onSearchInput}
    >
      <strong>Search:</strong>
    </InputWithLabel>

    <button
      type="submit"
      disabled={!searchTerm}
      className="button button_large" // Classes compostas
    >
      Submit
    </button>
  </form>
);

const InputWithLabel = ({ id, value, type = 'text', onInputChange, children }) => (
  <>
    <label htmlFor={id} className="label">
      {children}
    </label>
    &nbsp;
    <input
      id={id}
      type={type}
      value={value}
      onChange={onInputChange}
      className="input"
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
  // Adicionado className "item"
  <li className="item">
    {/* Estilos Inline para largura das colunas */}
    <span style={{ width: '40%' }}>
      <a href={item.url}>{item.title}</a>
    </span>
    <span style={{ width: '30%' }}>{item.author}</span>
    <span style={{ width: '10%' }}>{item.num_comments}</span>
    <span style={{ width: '10%' }}>{item.points}</span>
    <span style={{ width: '10%' }}>
      <button
        type="button"
        onClick={() => onRemoveItem(item)}
        className="button button_small"
      >
        Dismiss
      </button>
    </span>
  </li>
);

export default App;
```

### Análise Técnica

1. **`import './App.css'`**: O Vite configura o projeto para injetar esse CSS automaticamente no `<head>` da página quando o JS é carregado 1.
    
2. **`className`**: Usado em vez de `class`. No HTML final gerado, isso se tornará um atributo `class` normal2.
    
3. **`style={{ width: '40%' }}`**: A chave externa `{}` indica que entraremos em modo JavaScript. A chave interna `{}` é o objeto JavaScript contendo os estilos. Propriedades com hífen (ex: `background-color`) viram camelCase (ex: `backgroundColor`), embora aqui tenhamos usado apenas `width` 3.
    

Sua aplicação agora deve ter uma aparência profissional com fundo azulado, fontes maiores e itens alinhados em colunas.

---

Com a aplicação funcional, conectada à API e estilizada, você completou o ciclo de desenvolvimento. O próximo e último passo lógico para um "Crash Course" é colocar isso no ar.

Diga **next** para vermos como fazer o **Build e Deploy** (Página 274).