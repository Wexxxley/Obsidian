


---
O uso de `useReducer` é indicado quando múltiplos valores de estado pertencem ao mesmo domínio lógico (como `stories`, `isLoading` e `isError`, que pertencem ao domínio de "buscar dados").

Um **Reducer** é uma função pura que recebe o estado atual (`state`) e uma ação (`action`) e retorna um novo estado (`newState`).

Definimos o reducer fora do componente `App`. Inicialmente, ele lidará apenas com a definição das histórias buscadas.

![](../../attachments/Pasted%20image%2020251125143450.png)

```jsx
const storiesReducer = (state, action) => {
  if (action.type === 'SET_STORIES') {
    // Retorna o payload da ação como o novo estado
    return action.payload;
  } else {
    throw new Error();
  }
};
```
Uma ação geralmente possui um `type` (identificador) e um `payload` (dados opcionais).

No componente `App`, substituímos o `useState` pelo `useReducer`. Este hook aceita a função reducer e um estado inicial, retornando o estado atual e uma função de despacho (`dispatch`).
```jsx
const App = () => {
  // ...

  // O dispatch substitui o setStories
  const [stories, dispatchStories] = React.useReducer(
    storiesReducer,
    [] // Estado inicial
  );

  // ...
};
```

#### 3. Despachando Ações (Dispatching Actions)

Em vez de definir o estado explicitamente com um setter, despachamos uma ação descrevendo _o que_ aconteceu.

**No `useEffect` (Data Fetching):**

JavaScript

```jsx
React.useEffect(() => {
  setIsLoading(true);

  getAsyncStories()
    .then((result) => {
      // Despacha a ação 'SET_STORIES' com os dados recebidos
      dispatchStories({
        type: 'SET_STORIES',
        payload: result.data.stories,
      });
      setIsLoading(false);
    })
    .catch(() => setIsError(true));
}, []);
```

#### 4. Movendo Lógica para o Reducer

Atualmente, a lógica de remover uma história reside no handler `handleRemoveStory`. Com reducers, podemos mover essa lógica de negócio para dentro da função reducer, tornando o componente mais declarativo.

No App (Handler):

O handler apenas despacha a intenção de remover.

JavaScript

```
const handleRemoveStory = (item) => {
  dispatchStories({
    type: 'REMOVE_STORY',
    payload: item,
  });
};
```

No Reducer (Lógica):

O reducer intercepta a ação REMOVE_STORY e calcula o novo estado. O livro recomenda o uso de switch statements para gerenciar múltiplos tipos de ação de forma limpa.

JavaScript

```
const storiesReducer = (state, action) => {
  switch (action.type) {
    case 'SET_STORIES':
      return action.payload;
    case 'REMOVE_STORY':
      // A lógica de filtro migrou para cá
      return state.filter(
        (story) => action.payload.objectID !== story.objectID
      );
    default:
      throw new Error();
  }
};
```

Benefício Técnico:

Agora temos um único local (storiesReducer) que gerencia todas as transições de estado possíveis para as histórias. Isso facilita testes e manutenção, pois a lógica de atualização está desacoplada da UI 2.

---

Diga **next** para prosseguir para **React Impossible States**, onde unificaremos todos os estados relacionados (`stories`, `isLoading`, `isError`) em um único objeto de estado complexo para evitar bugs.