
---

Um **hook** é uma função especial no React que permite que você "se conecte" a funcionalidades do React, como o estado e o ciclo de vida de um componente.

Existem vários hooks nativos do React, mas os mais importantes são três: `useState`, `useEffect` e `useContext`.

---
#### **1. useState**
A função dele é permitir que você adicione estado a um componente funcional.

Em termos simples, o estado é uma "caixinha" de dados que o React vai monitorar. Quando o valor dessa caixinha muda, o React sabe que precisa atualizar o componente.

A função `useState` retorna um array com exatamente dois elementos:
1. O **valor atual** do estado.
2. Uma **função** para atualizar esse valor.
#### **Exemplo Prático: Um Contador**
```js
import React, { useState } from 'react';

function Contador() {
  const [count, setCount] = useState(0);

  // 2. Cria uma função para o clique do botão.
  const handleIncrement = () => {
    // 3. Usa a função 'setCount' para atualizar o estado.
    setCount(count + 1);
  };

  return (
    <div>
      <p>Você clicou {count} vezes</p>
      <button onClick={handleIncrement}>
        Clique para Incrementar
      </button>
    </div>
  );
}

export default Contador;
```

**Quando usar?** Use `useState` sempre que precisar que seu componente "lembre" de um valor e re-renderize quando esse valor mudar.

---
#### **2. useEffect**
É o hook que lida com **efeitos colaterais** em seu componente. Um efeito colateral é qualquer coisa que afeta o mundo "externo", como requisições de API e manipulação do DOM

Use `useEffect` para ações que precisam acontecer após o componente ser renderizado. 
    - Buscar dados de uma API quando o componente é carregado.
    - Manipular o título da página.

```js
import { useEffect } from 'react';

function MudarTitulo(props) {
  useEffect(() => {
    document.title = props.titulo;
  }, [titulo]); // O efeito é executado novamente quando 'titulo' muda.
  
  return <h1>{titulo}</h1>;
}
```

- O segundo argumento do `useEffect` é chamado de **array de dependências**. A função que você passa para o `useEffect` só será executada se uma das variáveis nesse array mudar.
- **Sem o array de dependências:** O `useEffect` seria executado **a cada renderização** do componente. Isso é ineficiente.
- **Com um array vazio `[]`:** O `useEffect` seria executado apenas uma vez.
    


---
#### 3. useContext
É o hook que permite acessar o valor de um **contexto** no React, evitando a necessidade de passar props manualmente através de vários níveis de componentes.
    
- **Quando usar?** Use `useContext` quando você precisa compartilhar um estado ou valor que é considerado "global" para uma parte da sua árvore de componentes, como:
    - O tema atual da aplicação (modo claro/escuro).
    - Informações de autenticação do usuário.
    - Preferências de idioma.

```js
import { useContext } from 'react';
import { ThemeContext } from './ThemeContext'; // Importando o contexto

function BotaoThema() {
  const theme = useContext(ThemeContext);

  return (
    <button style={{ background: theme.background, color: theme.foreground }}>
      Botão com tema
    </button>
  );
}
```

