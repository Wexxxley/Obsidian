

---

Seguindo a ordem do livro, chegamos ao capítulo **"React Custom Hooks (Advanced)"** (Hooks Personalizados).

Até agora, utilizamos os hooks nativos `useState` e `useEffect`. Quando temos uma lógica que envolve estado e efeitos colaterais que pode ser reutilizada, podemos encapsulá-la em nosso próprio Hook.

---

### **20. React Custom Hooks (Advanced) (Páginas 84-88)**

O objetivo técnico aqui é extrair a lógica de persistência de estado (sincronização com `localStorage`) do componente `App` para uma função reutilizável. Isso limpa o componente e modulariza a lógica.

#### Criação do Hook `useStorageState`

Um Custom Hook é apenas uma função JavaScript que:

1. Usa outros Hooks do React internamente.
    
2. Segue a convenção de nomeação começando com o prefixo `use`.
    

Extração da Lógica:

Movemos o useState e o useEffect para fora do App e para dentro da nova função useStorageState.

JavaScript

```
const useStorageState = (key, initialState) => {
  // 1. Inicialização Lenta (Lazy Initialization)
  // O estado interno agora é genérico ('value'), não mais específico ('searchTerm')
  const [value, setValue] = React.useState(
    localStorage.getItem(key) || initialState
  );

  // 2. Efeito Colateral
  // Dependências: O efeito roda se o 'value' mudar OU se a 'key' mudar
  React.useEffect(() => {
    localStorage.setItem(key, value);
  }, [value, key]);

  // 3. Retorno
  // Retornamos um array para manter a mesma API do useState, permitindo
  // que o consumidor do hook renomeie as variáveis na desestruturação.
  return [value, setValue];
};
```

**Pontos Técnicos Críticos:**

- **Parâmetros Genéricos:** O hook aceita `key` e `initialState` como argumentos, tornando-o agnóstico ao domínio (não sabe o que é "search", apenas sabe o que é uma chave e um valor).
    
- **Array de Dependências:** Note que `key` foi adicionado ao array de dependências `[value, key]`. Isso é crucial: se a chave de armazenamento mudar durante a vida útil do componente, o efeito deve rodar novamente para salvar os dados no local correto 1.
    

#### Integração no Componente `App`

Agora, o componente `App` consome este novo hook da mesma maneira que consumia o `useState`, mas passando a chave de armazenamento desejada.

JavaScript

```
const App = () => {
  const stories = [ ... ];

  // Uso do Custom Hook
  // A chave 'search' é passada para evitar conflitos no localStorage
  const [searchTerm, setSearchTerm] = useStorageState('search', 'React');

  const handleSearch = (event) => {
    setSearchTerm(event.target.value);
  };

  const searchedStories = stories.filter((story) =>
    story.title.toLowerCase().includes(searchTerm.toLowerCase())
  );

  return (
    <div>
      <h1>My Hacker Stories</h1>
      <Search search={searchTerm} onSearch={handleSearch} />
      <hr />
      <List list={searchedStories} />
    </div>
  );
};
```

Vantagem Arquitetural:

O componente App não conhece mais os detalhes de implementação do localStorage. Ele apenas sabe que possui um estado que é persistido (useStorageState). Se decidirmos mudar de localStorage para sessionStorage ou cookie no futuro, alteraremos apenas o hook, e todos os componentes que o utilizam serão atualizados automaticamente.

---

Diga **next** para prosseguir para **React Fragments**, onde aprenderemos a renderizar múltiplos elementos sem sujar o DOM com `divs` extras.