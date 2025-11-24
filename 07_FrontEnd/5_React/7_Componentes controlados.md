

---

Elementos de formulário HTML (como `<input>`, `<textarea>`, `<select>`) mantêm nativamente seu próprio estado interno no DOM. Quando você digita em um campo de texto, o navegador atualiza o valor visualmente, independentemente do React.

Atualmente, o componente `Search` é um **Uncontrolled Component**. O React recebe os eventos de mudança (`onChange`), mas não determina explicitamente o que está sendo exibido no input.

**Controlled Components**: Para resolver isso, devemos converter o input em um Componente Controlado. Isso significa que o React se torna a "**única fonte da verdade**". O valor exibido no input deve ser sempre uma reflexão direta do estado do React.

1. No `App`, passamos o valor atual de `searchTerm` como uma prop para o `Search`. 
2. No `Search`, atribuímos essa prop ao atributo `value` do elemento HTML `<input>`.


```jsx
const App = () => {
  const stories = [ ... ];

  // Inicializamos com um valor para demonstrar o controle
  const [searchTerm, setSearchTerm] = React.useState('React');

  const handleSearch = (event) => {
    setSearchTerm(event.target.value);
  };

  const searchedStories = stories.filter((story) =>
    story.title.toLowerCase().includes(searchTerm.toLowerCase())
  );

  return (
    <div>
      <h1>My Hacker Stories</h1>

      {/* Passamos o estado (search) E o callback (onSearch) */}
      <Search search={searchTerm} onSearch={handleSearch} />

      <hr />

      <List list={searchedStories} />
    </div>
  );
};

const Search = (props) => {
  return (
    <div>
      <label htmlFor="search">Search: </label>
      {/* Componente Controlado:
         1. value={props.search}: O React força o input a mostrar este valor.
         2. onChange={props.onSearch}: Qualquer tentativa de mudança dispara o evento.
      */}
      <input
        id="search"
        type="text"
        value={props.search}
        onChange={props.onSearch}
      />
    </div>
  );
};
```

**O Ciclo de Vida do Componente Controlado:**

1. **Renderização:** O input exibe o valor recebido via prop `value` (estado do React).
    
2. **Interação:** O usuário pressiona uma tecla. O input **não** muda seu valor visualmente sozinho de imediato. Ele dispara o evento `onChange`.
    
3. **Atualização:** O callback `handleSearch` atualiza o estado `searchTerm` no `App`.
    
4. **Re-renderização:** O React re-renderiza o `App` e o `Search` com o novo estado.
    
5. **Sincronização:** O React atualiza o atributo `value` do input com o novo caractere. Só agora o usuário vê a letra que digitou.
    

Ao adotar esse padrão, garantimos que o estado visual (DOM) e o estado lógico (React) estejam sempre perfeitamente sincronizados .