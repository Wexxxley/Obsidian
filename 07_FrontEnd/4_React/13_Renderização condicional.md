

---

### **1.Deixando os dados assíncronos**

Até agora, utilizamos dados síncronos. Em aplicações reais, os dados vêm de uma API remota e chegam de forma assíncrona. Antes de conectarmos a uma API real, simularemos esse comportamento para entender o ciclo de renderização assíncrono.

O objetivo técnico é transformar a lista `stories` de um estado inicial síncrono para um estado que começa vazio e é preenchido após a resolução de uma _Promise_.

**Simulação da API**: Foi criado uma função fora do componente que retorna uma Promise.
![](../../attachments/Pasted%20image%2020251125133327.png)

**Inicialização do Estado**: Mudamos a inicialização de `const [stories, setStories]`. Agora a aplicação inicia com uma lista vazia. 

**useEffect:**  Introduzimos o hook useEffect para disparar a busca dos dados. Note que o Array de dependências vazio, isso garante que essa busca aconteça apenas **uma vez**, quando o componente é montado (aparece na tela pela primeira vez) .
![](../../attachments/Pasted%20image%2020251125134436.png)

---

Com a introdução de dados assíncronos, criamos um problema de Experiência do Usuário: durante o atraso da requisição, a aplicação parece travada. Vamos focar em fornecer feedback visual (Loading e Erro) utilizando renderização condicional no JSX.

### **2. Loading State** 

Introduzimos um estado booleano `isLoading` para rastrear o status da requisição.
- **Fluxo no `useEffect`:**
    1. Antes de iniciar a Promise: `setIsLoading(true)`.
    2. Quando a Promise resolve: `setIsLoading(false)`.

### **3. Error State** 

Em aplicações reais, requisições falham. Introduzimos o estado `isError` para capturar falhas na Promise.
- **Fluxo:** Utilizamos o bloco `.catch()` da Promise para capturar erros e atualizar `setIsError(true)`.

### 4. Renderização Condicional

- **Operador Ternário (`? :`):** Ideal para situações "Se/Senão". Se `isLoading` for verdadeiro, renderiza o parágrafo de carregamento; caso contrário, renderiza o componente `List`.
    
- **Operador Lógico AND (`&&`):** Ideal para situações "Se/Nada". Se `isError` for verdadeiro, renderiza a mensagem de erro; caso contrário, não renderiza nada.    


```
const App = () => {
  // ... (stories state) ...

  const [searchTerm, setSearchTerm] = useStorageState('search', 'React');

  // 1. Novos Estados de Controle
  const [isLoading, setIsLoading] = React.useState(false);
  const [isError, setIsError] = React.useState(false);

  React.useEffect(() => {
    // Inicia o carregamento
    setIsLoading(true);

    getAsyncStories()
      .then((result) => {
        setStories(result.data.stories);
        // Finaliza o carregamento com sucesso
        setIsLoading(false);
      })
      .catch(() => {
        // Trata o erro caso a promise seja rejeitada
        setIsError(true);
        setIsLoading(false); // Finaliza o carregamento mesmo com erro
      });
  }, []);

  // ... (handlers) ...

  return (
    <div>
      <h1>Minha aplicação</h1>
      <InputWithLabel ... >
        Search:
      </InputWithLabel>

      <hr />

      {/* Renderização Condicional de Erro (Curto-circuito) */}
      {isError && <p>Something went wrong ...</p>}

      {/* Renderização Condicional de Loading (Ternário) */}
      {isLoading ? (
        <p>Loading ...</p>
      ) : (
        <List list={searchedStories} onRemoveItem={handleRemoveStory} />
      )}
    </div>
  );
};
```

**Resultado Visual:**

1. Ao recarregar a página, você verá "Loading ..." por 2 segundos.
    
2. Após 2 segundos, a lista aparecerá.
    
3. Se você modificar a função `getAsyncStories` para retornar `Promise.reject()`, verá a mensagem "Something went wrong ...".
    

---

Esta seção completa a base para lidar com dados assíncronos.

Diga **next** para prosseguir para **React Advanced State**, onde introduziremos o **Reducer** para gerenciar esses múltiplos estados (`stories`, `isLoading`, `isError`) de forma mais organizada e robusta.