

---
### **1. React State**

Enquanto props são usadas para passar informações, o state é usado para gerenciar informações que mudam ao longo do tempo dentro de um componente.

**Hook useState:** O `useState` é um React Hook que permite adicionar estado a componentes funcionais.
![](../../attachments/Pasted%20image%2020251124063152.png)

1. **Inicialização:** O `useState('')` define o valor inicial.
2. **Interação:** O usuário digita, disparando `handleChange`.
3. **Atualização:** `setSearchTerm` é chamado com o novo valor.
4. **Re-renderização:** O React detecta a mudança de estado e re-executa a função do componente `Search`. O valor atualizado de `searchTerm` é refletido no JSX .

---
### **2. A Mecânica do useState**

Quando você escreve:
```jsx
const [searchTerm, setSearchTerm] = React.useState('');
```
Está acontecendo o seguinte:

1. **React.useState('')**: Você solicita ao React um espaço na memória associado a este componente específico. O valor inicial é `''`.
    
2. **O Retorno (Array Destructuring)**: O Hook retorna um array com exatamente dois itens 7:
    
    - **Índice 0 (`searchTerm`):** O valor atual armazenado na memória do React. (Leitura).
        
    - **Índice 1 (`setSearchTerm`):** Uma função específica para atualizar esse valor. (Escrita).
        

**O Fluxo de Atualização (Técnico):**

1. **O Evento:** O usuário digita no input. O evento `onChange` dispara.
    
2. **O Handler:** Sua função `handleChange` captura o texto (`event.target.value`).
    
3. **A Escrita:** Você chama `setSearchTerm('novo texto')`.
    
4. **O Gatilho:** Ao chamar essa função de atualização, o React marca o componente como "sujo" (precisa de atualização)8.
    
5. **A Re-renderização:** O React executa a função `App` inteira novamente.
    
6. **A Persistência:** Desta vez, quando a linha `const [searchTerm...] = useState('')` é executada, o React _ignora_ o valor inicial `''` e devolve o valor que foi salvo na memória ('novo texto')9.
    
7. **O DOM:** O JSX é retornado com o novo valor e o navegador atualiza o HTML.
    

---

### **Resumo Técnico**

- **State:** É necessário porque variáveis locais morrem quando a função do componente termina de rodar. O State persiste os dados na memória do React entre renderizações.
    
- **Hook:** É a API (interface) que permite acessar essa memória interna de dentro de uma função.
    
- **`setFunction`:** É o gatilho que força o React a executar a função do componente novamente para atualizar a interface 10.
    

---

Diga **next** para prosseguir para **Lifting State in React**.
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