

---

O arquivo `src/main.jsx` é o ponto de conexão entre o React e o DOM nativo do navegador.
```jsx
import { createRoot } from 'react-dom/client';
import App from './App.jsx';

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

- **createRoot:** Método que inicializa a árvore de renderização do React concorrente.
- **document.getElementById('root'):** Seleciona a div vazia no index.html onde a aplicação será injetada.
- **render(<App />):** Instancia o componente raiz, iniciando o processo de renderização recursiva de toda a árvore de componentes.

---

### **11. React Component Declaration (Páginas 41-44)**

O livro propõe a refatoração das declarações de função padrão (`function App()`) para **Arrow Functions**, alinhando-se aos padrões modernos de JavaScript (ES6+).

**Refatoração para Arrow Functions:**

JavaScript

```
const App = () => {
  return (
    <div>...</div>
  );
};
```

Concise Body (Retorno Implícito):

Se o componente não possui lógica antes do return (apenas retorna JSX diretamente), pode-se omitir as chaves {} e a palavra-chave return 9.

JavaScript

```
const Search = () => (
  <div>
    <label htmlFor="search">Search: </label>
    <input id="search" type="text" />
  </div>
);
```

Esta forma é utilizada no livro para componentes "stateless" ou puramente visuais, tornando o código mais limpo.

---

Diga **next** para prosseguir para os tópicos de interação (Event Handlers e State).