

---
Até agora, utilizamos dados síncronos. Em aplicações reais, os dados vêm de uma API remota e chegam de forma assíncrona. Antes de conectarmos a uma API real, simularemos esse comportamento para entender o ciclo de renderização assíncrono.

O objetivo técnico é transformar a lista `stories` de um estado inicial síncrono para um estado que começa vazio e é preenchido após a resolução de uma _Promise_.

#### 1. Simulando a API (Promise)

Primeiro, removemos a variável `initialStories` e criamos uma função que retorna uma **Promise**.

JavaScript

```jsx
const initialStories = [ ... ]; // Mantemos os dados aqui apenas como "banco de dados"

// Função que simula uma requisição assíncrona
const getAsyncStories = () =>
  // Retorna uma Promise que resolve com um objeto contendo os dados
  Promise.resolve({ data: { stories: initialStories } });
```

#### 2. Buscando os Dados (`useEffect`)

No componente `App`, o estado `stories` agora deve ser inicializado como uma lista vazia `[]`, pois no momento da montagem do componente, os dados ainda não chegaram.

Utilizamos o hook **`useEffect`** para disparar a busca dos dados assim que o componente for montado.

JavaScript

```
const App = () => {
  // ... useStorageState ...

  // Estado inicial vazio (estado síncrono)
  const [stories, setStories] = React.useState([]);

  // Efeito para buscar dados (assíncrono)
  React.useEffect(() => {
    getAsyncStories().then((result) => {
      setStories(result.data.stories);
    });
  }, []); // Array de dependências vazio: executa apenas na montagem (mount)

  // ... handlers ...

  return ( ... );
};
```

**Fluxo de Renderização:**

1. **Mount:** O componente renderiza com `stories` vazio. O usuário vê uma lista vazia.
    
2. **Effect:** O `useEffect` executa `getAsyncStories`.
    
3. **Promise Resolve:** A promise resolve (instantaneamente, por enquanto).
    
4. **State Update:** `setStories` atualiza o estado com os dados recebidos.
    
5. **Re-render:** O componente renderiza novamente, agora com a lista preenchida.
    

#### 3. Simulando Latência (Delay Real)

Para tornar a simulação realista (uma requisição de rede nunca é instantânea), adicionamos um atraso artificial usando `setTimeout` dentro da Promise.

JavaScript

```
const getAsyncStories = () =>
  new Promise((resolve) =>
    setTimeout(
      () => resolve({ data: { stories: initialStories } }),
      2000 // Atraso de 2 segundos (2000ms)
    )
  );
```

Agora, ao recarregar a página, você perceberá um comportamento visual distinto: a aplicação carrega vazia, aguarda 2 segundos, e só então a lista aparece 1.

Isso expõe uma falha de UX (Experiência do Usuário): o usuário não sabe se a aplicação travou ou se está carregando. Isso nos leva ao próximo passo.

---

Diga **next** para prosseguir para **React Conditional Rendering**, onde implementaremos um indicador de carregamento (Loading State).