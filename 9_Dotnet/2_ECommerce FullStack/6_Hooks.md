
---

Um **hook** é uma função especial no React que permite que você "ganche" ou "se conecte" a funcionalidades do React, como o estado e o ciclo de vida de um componente.

Antes dos hooks, a única maneira de ter estado e funcionalidades de ciclo de vida em um componente era usando classes. Com os hooks, agora você pode fazer tudo isso em componentes funcionais, o que torna o código mais simples e limpo.

---

### Tipos Básicos de Hooks e Quando Usá-los

Existem vários hooks nativos do React, mas os mais importantes para começar são três: `useState`, `useEffect` e `useContext`.

#### 1. `useState`

- **O que é?** O hook que adiciona **estado** a um componente funcional. Ele retorna um array com duas posições: o valor atual do estado e uma função para atualizá-lo.
    
- **Quando usar?** Use `useState` sempre que precisar que seu componente "lembre" de um valor e re-renderize quando esse valor mudar. Por exemplo:
    
    - Gerenciar o valor de um input de formulário.
        
    - Controlar se um menu dropdown está aberto ou fechado.
        
    - Manter a contagem em um botão de contador.
        

JavaScript

```
import { useState } from 'react';

function Contador() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Você clicou {count} vezes
    </button>
  );
}
```

---

#### 2. `useEffect`

- **O que é?** O hook que lida com **efeitos colaterais** em seu componente. Um efeito colateral é qualquer coisa que afeta o mundo "externo" do seu componente, como requisições de API, manipulação do DOM ou listeners de eventos.
    
- **Quando usar?** Use `useEffect` para ações que precisam acontecer após o componente ser renderizado. Por exemplo:
    
    - Buscar dados de uma API quando o componente é carregado.
        
    - Configurar e limpar listeners de eventos (por exemplo, em um componente que reage ao redimensionamento da janela).
        
    - Manipular o título da página.
        

JavaScript

```
import { useEffect } from 'react';

function MudarTitulo({ titulo }) {
  useEffect(() => {
    // Este código será executado após a renderização do componente.
    document.title = titulo;
  }, [titulo]); // O efeito é executado novamente quando 'titulo' muda.
  
  return <h1>{titulo}</h1>;
}
```

---

#### 3. `useContext`

- **O que é?** O hook que permite acessar o valor de um **contexto** no React, evitando a necessidade de passar props manualmente através de vários níveis de componentes.
    
- **Quando usar?** Use `useContext` quando você precisa compartilhar um estado ou valor que é considerado "global" para uma parte da sua árvore de componentes, como:
    
    - O tema atual da aplicação (modo claro/escuro).
        
    - Informações de autenticação do usuário.
        
    - Preferências de idioma.
        

JavaScript

```
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

---

Em resumo, hooks são a forma moderna de construir componentes React, trazendo simplicidade e poder para o desenvolvimento de componentes funcionais. Dominar esses três hooks é o primeiro e mais importante passo para se tornar um desenvolvedor React.
### **useState**
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
