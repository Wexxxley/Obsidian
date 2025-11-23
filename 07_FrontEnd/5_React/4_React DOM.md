

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

