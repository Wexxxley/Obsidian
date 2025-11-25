

---
No React, a estilização funciona de forma muito similar ao HTML padrão, mas com duas diferenças  que você precisa memorizar:

1. **clas vira className**
2. **Estilos Inline são Objetos:** Ao usar o atributo `style`, você não passa uma string (`"color: red"`), mas sim um objeto JavaScript (`{{ color: 'red' }}`).

### **1. A Orquestração dos Arquivos**

**main.jsx e index.css**: main.jsx é o ponto de entrada da aplicação React. 
- Ele importa o componente raiz (App). 
- Ele importa o estilo global (index.css).
- Ele injeta toda a aplicação na div com id root do seu HTML.
- **index.css** Contém estilos globais que o Vite injeta na página inteira. As regras aqui afetam todos os elementos da aplicação, a menos que sejam sobrescritas por estilos mais específicos.

**App.jsx App.css**: App.jsx é onde toda a sua lógica React reside, ele importa o App.css
- **App.css:** Contém estilos específicos para os componentes definidos em App.jsx. 

Para que a estilização funcione corretamente é preciso:

1. **Conectar o CSS ao Componente**
	No arquivo App.jsx, adicione a importação do CSS logo abaixo da importação do React.
	![](../../attachments/Pasted%20image%2020251125185751.png)

2. **Adicionar as Classes className no JSX**
	O CSS define classes (ex: `.container`, `.button`), mas o seu JSX atual não está usando essas classes. Você precisa adicionar o atributo `className` aos elementos correspondentes.
	
	**Em `App`:**
	
	JavaScript
	
	```
	return (
	  // Adicione className="container"
	  <div className="container">
	    {/* Adicione className="headline-primary" */}
	    <h1 className="headline-primary">My Hacker Stories</h1>
	    
	    {/* ... resto do código ... */}
	  </div>
	);
	```
	
	**Em `SearchForm`:**
	
	JavaScript
	
	```
	const SearchForm = ({ searchTerm, onSearchInput, onSearchSubmit }) => (
	  // Adicione className="search-form"
	  <form onSubmit={onSearchSubmit} className="search-form">
	    {/* ... */}
	    
	    <button 
	      type="submit" 
	      disabled={!searchTerm}
	      className="button button_large" // Adicione as classes de botão
    >	
	      Submit
	    </button>
	  </form>
	);
	```
	
	**Em `InputWithLabel`:**
	
	JavaScript
	
	```
	const InputWithLabel = ({ id, value, type = 'text', onInputChange, children }) => (
	  <>
	    {/* Adicione className="label" */}
	    <label htmlFor={id} className="label">{children}</label>
	    &nbsp;
	    <input
	      id={id}
	      type={type}
	      value={value}
	      onChange={onInputChange}
	      className="input" // Adicione className="input"
	    />
	  </>
	);
	```
	
	**Em `Item`:**
	
	JavaScript
	
	```
	const Item = ({ item, onRemoveItem }) => (
	  // Adicione className="item"
	  <li className="item">
	    {/* Adicione estilos inline para largura das colunas */}
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
	        className="button button_small" // Adicione classes de botão
      >	
	        Dismiss
	      </button>
	    </span>
	  </li>
	);
	```

#### **Passo C: Limpar Conflitos do `index.css` (Opcional mas Recomendado)**

O arquivo `index.css` que veio com o Vite tem estilos padrão (fundo escuro `#242424`, centralização flexbox no `body`) que podem brigar com o seu `App.css` (fundo gradiente azul).

Para garantir que o estilo do livro prevaleça:

1. Abra `src/index.css`.
    
2. Você pode apagar tudo ou comentar as linhas conflitantes (principalmente `background-color`, `color` e o `display: flex` do `body`).
    
3. Ou simplesmente confie que o `.container` do `App.css` vai cobrir a tela toda (`height: 100vw` e `padding: 20px`).
    

### **Resumo da Ação**

1. **Importe** `import './App.css';` no topo de `App.jsx`.
    
2. **Preencha** os atributos `className="..."` nos elementos JSX conforme mostrei acima.
    
3. **Salve** todos os arquivos.
    

Se você fizer isso, sua aplicação passará de um HTML cru para uma interface estilizada com gradiente azul e itens alinhados.

---

Diga **next** para prosseguir para **Build Process** (Página 275), onde prepararemos essa aplicação para publicação.

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