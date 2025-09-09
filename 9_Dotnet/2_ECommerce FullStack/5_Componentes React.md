
#Concluded 

---
**O objetivo principal dos componentes é quebrar a UI em pedaços isolados.** Em vez de ter uma única página HTML gigante, você pode ter um componente para a barra de navegação, um para a barra lateral, um para cada card de produto, e até mesmo um para um simples botão.

---
### **1. Functional Components - O Padrão Moderno**
São simplesmente funções JavaScript que aceitam um objeto e retornam JSX, que descreve o que deve ser renderizado na tela. 

```jsx
    function Saudacao(props) {
      return <h1>Olá, {props.nome}!</h1>;
    }
    ```

---
### **2 Props (Properties)**
São a maneira de um componente **pai** passar dados para um componente **filho**. Pense neles como as "configurações" de um componente.

```jsx
// 1. O componente filho
function BookCard(props) {
  return (
    <div className="card">
      <h2>{props.titulo}</h2>
      <p>por {props.autor}</p>
    </div>
  );
}

// 2. O componente pai
// Ele passa as props como se fossem atributos HTML.
function App() {
  return (
    <div>
      <BookCard titulo="O Senhor dos Anéis" autor="J.R.R. Tolkien" />
      <BookCard titulo="Duna" autor="Frank Herbert" />
    </div>
  );
}
```

---
### **3. State**
É a "memória" interna de um componente. São dados que o próprio componente gerencia e que podem mudar ao longo do tempo, geralmente em resposta a uma interação do usuário.

- Quando o estado de um componente muda, o React automaticamente renderiza o componente na tela para refletir essa mudança. 
- Em componentes funcionais, usamos o **Hook** `useState` para adicionar estado.

```jsx
import { useState } from 'react'; // Importa o hook useState

function Counter() {
  // 1. Declara uma variável de estado chamada 'count'.
  // 'useState(0)' define o valor inicial como 0.
  // 'setCount' função usada para ATUALIZAR o estado.
  const [count, setCount] = useState(0);

  // 2. Chama a função de atualização.
  function handleIncrement() {
    setCount(count + 1);
  }
  
  return (
    <div>
      <p>Você clicou {count} vezes.</p>
      <button onClick={handleIncrement}>
        Clique aqui!!!
      </button>
    </div>
  );
}
```

---
### **4. Composição**
A verdadeira força dos componentes é a **composição**. Você cria componentes pequenos e focados e os combina para formar componentes maiores, até construir sua aplicação inteira.

**Exemplo de Composição:** Um componente `BookList` que reutiliza o `BookCard` para exibir uma lista de livros.
```jsx
function BookList() {
  const livros = [
    { id: 1, titulo: "1984", autor: "George Orwell" },
    { id: 2, titulo: "Fahrenheit 451", autor: "Ray Bradbury" },
    { id: 3, titulo: "Admirável Mundo Novo", autor: "Aldous Huxley" }
  ];

  return (
    <section>
      <h1>Minha Lista de Leitura</h1>
      <div>
        {livros.map(livro => (
          <BookCard key={livro.id} titulo={livro.titulo} autor={livro.autor} />
        ))}
      </div>
    </section>
  );
}
```

---
### **5. Mais exemplos**

Usando map e a tag Fragment
![](attachments/Pasted%20image%2020250814092647.png)

2. `addProduct`: Adicionando um Novo Item (A Forma Correta)

```
const addProduct = () => {
  setProducts(prevState => [...prevState, {name: 'product3', price: 300.00}])
}
```


#### a) Imutabilidade e o Spread Syntax (`...`)

O princípio mais importante do React é a **imutabilidade**. Você **nunca deve modificar o estado diretamente**. Em vez disso, você deve criar uma **cópia** do estado, fazer suas alterações na cópia e então usar a função de atualização (`setProducts`) para substituir o estado antigo pelo novo.

O código `[...prevState, { ... }]` faz exatamente isso:

- **`...prevState`**: O **spread syntax (`...`)** pega todos os itens do array de produtos antigo (`prevState`) e os "espalha" dentro de um novo array.
    
- **`[...]`**: Isso cria um array completamente **novo** em memória.
    
- **, `{name: 'product3', ...}`**: Em seguida, ele adiciona o novo produto ao final deste **novo** array.
    

O resultado é um array totalmente novo que contém todos os produtos antigos mais o novo.

#### b) "Functional Update" (Atualização Funcional)

Em vez de passar o novo array diretamente para `setProducts`, o código usa uma função: `prevState => ...`.

- **`setProducts(função)`**: Esta é a forma mais segura de atualizar o estado, especialmente quando o novo estado depende do estado anterior.
    
- **`prevState`**: O React garante que o `prevState` dentro desta função será sempre o valor **mais recente** do estado, evitando bugs de "estado obsoleto" (stale state) que podem acontecer em operações complexas ou assíncronas.
    

### Resumo do Fluxo

1. A função `addProduct` é chamada (provavelmente por um clique de botão).
    
2. Ela executa `setProducts`, passando uma função como argumento.
    
3. O React fornece o estado atual (`prevState`, que é `[{...}, {...}]`) para essa função.
    
4. Dentro da função, um **novo** array é criado usando o spread syntax, resultando em `[{...}, {...}, {name: 'product3', ...}]`.
    
5. O React recebe este novo array, substitui o estado antigo e renderiza novamente o componente na tela para mostrar a lista atualizada com os três produtos.