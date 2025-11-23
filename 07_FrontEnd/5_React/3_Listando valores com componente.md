

---



A renderização de listas em React utiliza o JavaScript nativo. O método map() de arrays é o padrão para iterar sobre dados e retornar elementos JSX.

Inicialmente, a lista de dados é definida como uma variável fora do componente, simulando dados que viriam de uma API JSON.

![](../../attachments/Pasted%20image%2020251123171205.png)

Dentro do JSX, utiliza-se chaves {} para executar o código JavaScript. O método map itera sobre cada objeto item da lista e retorna um elemento 1.
![](../../attachments/Pasted%20image%2020251123171325.png)

O React exige que cada elemento renderizado via iteração de array possua um atributo key.

- **Propósito Técnico:** O `key` é um identificador estável que permite ao algoritmo de reconciliação do React rastrear quais itens mudaram, foram adicionados ou removidos. Isso otimiza a performance de re-renderização 2.
    
- **Valor do `key`:** Deve ser um identificador único e estável (como `item.objectID`). O uso do índice do array (`index`) é desencorajado, pois a reordenação da lista pode causar problemas de performance e bugs de estado no componente 3.
    

---

### **8. Meet another React Component (Páginas 32-35)**

À medida que a aplicação cresce, manter toda a lógica no componente `App` torna-se insustentável. O processo de refatoração envolve extrair partes da UI para componentes dedicados.

Extração do Componente List:

A responsabilidade de renderizar a lista é movida para um novo componente.

JavaScript

```
function List() {
  return (
    <ul>
      {list.map(function (item) {
        return (
           // ... conteúdo do item da lista com key ...
           <li key={item.objectID}>...</li>
        );
      })}
    </ul>
  );
}
```

Extração do Componente Search:

Os elementos de input e label são movidos para um componente Search.

JavaScript

```
function Search() {
  return (
    <div>
      <label htmlFor="search">Search: </label>
      <input id="search" type="text" />
    </div>
  );
}
```

Composição no App:

O componente App passa a atuar como um orquestrador, instanciando os componentes filhos 4.

JavaScript

```
function App() {
  return (
    <div>
      <h1>My Hacker Stories</h1>
      <Search />
      <hr />
      <List />
    </div>
  );
}
```

Hierarquia de Componentes (Component Tree):

Esta estrutura cria uma árvore onde:

- `App` é o **Parent Component** (componente pai) ou Root.
    
- `List` e `Search` são **Child Components** (filhos) de `App` e **Sibling Components** (irmãos) entre si.
    
- Componentes que não renderizam outros componentes são chamados de **Leaf Components** (folhas)5.
    

---

### **9. React Component Instantiation (Páginas 36-38)**

O livro formaliza a distinção entre declaração e instância:

- **Component Declaration (Declaração):** É a definição da função (o código fonte). Ex: `function List() { ... }`. É o "blueprint"6.
    
- **Component Instantiation (Instanciação):** Ocorre quando o componente é invocado dentro do JSX usando a sintaxe de tag `<List />`. O React cria uma instância desse componente para ser montada no DOM. É possível criar múltiplas instâncias independentes a partir de uma única declaração 7.
    

---

### **10. React DOM (Páginas 39-40)**

O arquivo `src/main.jsx` é o ponto de conexão entre o React e o DOM nativo do navegador.

JavaScript

```
import { createRoot } from 'react-dom/client';
import App from './App.jsx';

createRoot(document.getElementById('root')).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

- **`createRoot`:** Método da biblioteca `react-dom/client` que inicializa a árvore de renderização do React concorrente.
    
- **`document.getElementById('root')`:** Seleciona a `div` vazia no `index.html` onde a aplicação será injetada.
    
- **`render(<App />)`:** Instancia o componente raiz, iniciando o processo de renderização recursiva de toda a árvore de componentes 8.
    

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