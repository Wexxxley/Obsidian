
#Concluded 

---
**O objetivo principal dos componentes é quebrar a UI em pedaços isolados.** Em vez de ter uma única página HTML gigante, você pode ter um componente para a barra de navegação, um para a barra lateral, um para cada card de produto, e até mesmo um para um simples botão.

### **1. Tipos de Componentes**

Existem duas maneiras de criar componentes em React.  Hoje em dia, uma é a forma recomendada.

1. **Functional Components - O Padrão Moderno**: São simplesmente funções JavaScript que aceitam um objeto e retornam JSX, que descreve o que deve ser renderizado na tela. 

    ```jsx
    function Saudacao(props) {
      return <h1>Olá, {props.nome}!</h1>;
    }
    ```

2. **Class Components - O Jeito Antigo**: Você ainda os encontrará em projetos mais antigos, mas raramente precisará criar novos.
    ```jsx
    class Saudacao extends React.Component {
      render() {
        return <h1>Olá, {this.props.nome}!</h1>;
      }
    }
    ```



---
### **2 Props (Properties)**
São a maneira de um componente **pai** passar dados para um componente **filho**. Pense neles como as "configurações" de um componente.
- As props são **somente leitura**. 

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