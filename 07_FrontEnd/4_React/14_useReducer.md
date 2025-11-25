


---
O uso de `useReducer` é indicado quando múltiplos valores de estado pertencem ao mesmo domínio lógico (como `stories`, `isLoading` e `isError`, que pertencem ao domínio de "buscar dados").

Um **Reducer** é uma função que recebe o estado atual (`state`) e uma ação (`action`) e retorna um novo estado (`newState`).

Definimos o reducer fora do componente `App`.
![](../../attachments/Pasted%20image%2020251125143450.png)
Uma ação geralmente possui um `type` (identificador) e um `payload` (dados opcionais).

No componente `App`, substituímos o `useState` pelo `useReducer`. Este hook aceita a função reducer e um estado inicial, retornando o estado atual e uma função de despacho (`dispatch`).
![](../../attachments/Pasted%20image%2020251125143604.png)

Em vez de definir o estado explicitamente com um setter, despachamos uma ação descrevendo _o que_ aconteceu.

Com reducers, podemos mover essa lógica de negócio para dentro da função reducer, tornando o componente mais declarativo.

Agora temos um único local (storiesReducer) que gerencia todas as transições de estado possíveis para as histórias. Isso facilita testes e manutenção, pois a lógica de atualização está desacoplada da UI 2.
