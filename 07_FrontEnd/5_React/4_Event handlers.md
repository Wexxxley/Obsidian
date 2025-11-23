


---
### **1. Event Handlers**

Para adicionar interatividade, o React utiliza **Event Handlers**.  Diferente do HTML nativo (onclick), o React utiliza a convenção camelCase para eventos (onClick, onChange) e espera uma função.

**Synthetic Events:** O React não passa eventos nativos do navegador para os handlers. Ele encapsula o evento nativo em um **SyntheticEvent**. Isso garante compatibilidade entre diferentes navegadores e otimiza a performance .

**Implementação no Componente Search:** Define-se uma função handleChange dentro do componente para capturar a interação.
![](../../attachments/Pasted%20image%2020251123193132.png)
Deve-se passar a referência da função, não a sua execução.
- **Correto:** onChange={handleChange}. Passa a func para ser executada quando o evento ocorrer
- **Incorreto:** onChange={handleChange()}. Executa a função durante a renderização.

Nesse exemplo, toda vez que digito algo no input, o console imprime.
![](../../attachments/Pasted%20image%2020251123193353.png)

---
### **2. React Props**

As Props são o mecanismo para passar dados de um componente pai para um componente filho.

**Refatoração da Lista:** A variável stories (anteriormente list) é movida para o escopo do componente `App` e passada para o componente `List` via atributo JSX.

JavaScript

```js
const App = () => {
  const stories = [ ... ]; // Vetor de dados definido aqui

  return (
    <div>
      <h1>My Hacker Stories</h1>
      <Search />
      <hr />
      <List list={stories} />
    </div>
  );
};
```

**Recebendo Props:** O componente filho recebe um objeto `props` como primeiro argumento da função. As propriedades passadas no JSX tornam-se chaves desse objeto.

JavaScript

```
const List = (props) => (
  <ul>
    {props.list.map((item) => (
      <Item key={item.objectID} item={item} />
    ))}
  </ul>
);
```

**Imutabilidade:** Props são **imutáveis** (read-only). Um componente filho nunca deve alterar as props recebidas. Elas servem estritamente para o fluxo de dados unidirecional (top-down) .

**Extração do Componente Item:** O livro demonstra a extração de um componente `Item` para encapsular a renderização de cada linha, recebendo o objeto `item` específico via props.

JavaScript

```
const Item = (props) => (
  <li>
    <span>
      <a href={props.item.url}>{props.item.title}</a>
    </span>
    {/* ... outros campos ... */}
  </li>
);
```

---

### **14. React State (Páginas 52-56)**

Enquanto props são usadas para passar informações, o **State** (estado) é usado para gerenciar informações que mudam ao longo do tempo dentro de um componente.

**Hook `useState`:** O `useState` é um React Hook que permite adicionar estado a componentes funcionais.

JavaScript

```
const Search = () => {
  // Desestruturação de array: [estadoAtual, funçãoAtualizadora]
  const [searchTerm, setSearchTerm] = React.useState('');

  const handleChange = (event) => {
    // Atualiza o estado com o valor do input
    setSearchTerm(event.target.value);
  };

  return (
    <div>
      <label htmlFor="search">Search: </label>
      <input id="search" type="text" onChange={handleChange} />
      <p>
        Searching for <strong>{searchTerm}</strong>.
      </p>
    </div>
  );
};
```

**Ciclo de Renderização:**

1. **Inicialização:** O `useState('')` define o valor inicial.
    
2. **Interação:** O usuário digita, disparando `handleChange`.
    
3. **Atualização:** `setSearchTerm` é chamado com o novo valor.
    
4. **Re-renderização:** O React detecta a mudança de estado e re-executa a função do componente `Search`. O valor atualizado de `searchTerm` é refletido no JSX .
    

O livro enfatiza que a atualização de estado é o gatilho primário para a re-renderização da interface do usuário (UI).

---

### **15. Callback Handlers in JSX (Páginas 57-59)**

O fluxo de dados no React é unidirecional (pai para filho via props). Para que um filho comunique uma mudança para o pai (ex: o `Search` informar o `App` sobre o termo pesquisado), utiliza-se o padrão de **Callback Handler**.

**Conceito:**

1. O componente Pai (`App`) define uma função de callback (`handleSearch`).
    
2. O Pai passa essa função como prop para o Filho (`Search`).
    
3. O Filho executa essa função prop quando o evento ocorre.
    

**Implementação no Pai (App):**

JavaScript

```
const App = () => {
  const stories = [ ... ];

  // Callback definido no Pai
  const handleSearch = (event) => {
    console.log(event.target.value);
  };

  return (
    <div>
      <h1>My Hacker Stories</h1>
      {/* Passagem do callback via prop 'onSearch' */}
      <Search onSearch={handleSearch} />
      <hr />
      <List list={stories} />
    </div>
  );
};
```

**Implementação no Filho (Search):**

JavaScript

```
const Search = (props) => {
  const [searchTerm, setSearchTerm] = React.useState('');

  const handleChange = (event) => {
    setSearchTerm(event.target.value);
    // Execução do callback recebido via props, "subindo" o evento
    props.onSearch(event);
  };

  return (
    <div>
      <label htmlFor="search">Search: </label>
      <input id="search" type="text" onChange={handleChange} />
      {/* ... */}
    </div>
  );
};
```

Isso estabelece um canal de comunicação onde o componente filho controla quando o evento ocorre, mas a lógica de resposta ao evento (ou parte dela) reside no componente pai.

---

Diga **next** para prosseguir com tópicos avançados de estado e componentes (Lifting State, Controlled Components).