

---

O componente Search atual tem dois defeitos principais de arquitetura:

1. **Acoplamento ao Domínio:** Ele "sabe" que é uma busca (o label é fixo como "Search").
2. **Duplicação de IDs:** Se renderizarmos dois componentes `Search` na mesma página, teremos dois elementos HTML com `id="search"`. Isso viola a regra do HTML de IDs únicos.
 
Vamos renomear o componente para InputWithLabel e tornar dinâmicas todas as propriedades que o prendem a um caso de uso específico. O componente agora aceita `id`, `label`, `value`, `type` e `onInputChange` como props.


```jsx
// Renomeado de 'Search' para 'InputWithLabel'
// Recebe props genéricas para desacoplar da lógica de "Busca"
const InputWithLabel = ({id,
  label,
  value,
  type = 'text', // Parâmetro padrão: se não for passado, assume 'text'
  onInputChange,
}) => (
  <>
    <label htmlFor={id}>{label}</label>
    &nbsp;
    <input
      id={id}
      type={type}
      value={value}
      onChange={onInputChange}
    />
  </>
);
```

**Detalhes Técnicos:**

- **Parâmetro Padrão (Default Parameter):** Na assinatura da função, `type = 'text'` garante que o componente funcione mesmo se o desenvolvedor esquecer de passar a prop `type`. É uma funcionalidade do ES6 aplicada ao React 2.
    
- **ID Dinâmico:** A prop `id` é usada tanto no atributo `htmlFor` do label quanto no `id` do input, garantindo que o vínculo de acessibilidade seja único para cada instância.
    

#### Atualização do Consumo no `App`

Agora precisamos atualizar o `App` para usar esse novo componente genérico, passando os dados específicos da busca.

JavaScript

```
const App = () => {
  const [searchTerm, setSearchTerm] = useStorageState('search', 'React');

  const handleSearch = (event) => {
    setSearchTerm(event.target.value);
  };

  // ... lógica de filtro ...

  return (
    <div>
      <h1>My Hacker Stories</h1>

      {/* Instanciação com dados específicos de Busca */}
      <InputWithLabel
        id="search"
        label="Search"
        value={searchTerm}
        onInputChange={handleSearch}
      />

      <hr />
      <List list={searchedStories} />
    </div>
  );
};
```

Trade-off (Compromisso):

Ao generalizar, aumentamos a API de Superfície do componente (ele precisa de mais props para funcionar). Perdemos a simplicidade de <Search /> (que já sabia tudo o que tinha que fazer), mas ganhamos um componente que pode criar qualquer campo de texto na aplicação. É o equilíbrio entre Especialização vs. Generalização 3.

---

Diga **next** para prosseguir para **React Component Composition**, onde aprenderemos a passar elementos _dentro_ das tags do componente (como filhos), em vez de apenas via atributos.