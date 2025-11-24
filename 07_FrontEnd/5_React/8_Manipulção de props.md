

---

### **1. Destructuring**

A desestruturação de objetos permite extrair propriedades de um objeto diretamente para variáveis.

Em vez de acessar props dentro da função, desestruturamos o objeto diretamente na assinatura da função. Isso torna explícito quais dados o componente requer para funcionar.
![](../../attachments/Pasted%20image%2020251124140211.png)
Isso elimina a necessidade de usar `props.` em todo lugar e também remove a necessidade do bloco de corpo da função (`{ ... }` e `return`) se o componente apenas retornar JSX 1.

#### 2. Nested Destructuring (Desestruturação Aninhada)

O livro explora um caso mais complexo no componente `Item`. O `Item` recebe um objeto `item` dentro das props. Podemos desestruturar o `item` e, simultaneamente, desestruturar as propriedades de dentro dele (`title`, `url`, etc.).

JavaScript

```
// Variação: Desestruturação Aninhada (Página 73)
const Item = ({
  item: {
    title,
    url,
    author,
    num_comments,
    points,
  },
}) => (
  <li>
    <span>
      <a href={url}>{title}</a>
    </span>
    <span>{author}</span>
    <span>{num_comments}</span>
    <span>{points}</span>
  </li>
);
```

**Nota Técnica:** O livro observa que, embora possível, a desestruturação aninhada pode introduzir muito ruído ("clutter") e indentação na assinatura da função, prejudicando a legibilidade em certos casos 2.

#### 3. Spread and Rest Operators (Operadores Spread e Rest)

Esta é uma técnica avançada para passar props adiante.

- **Spread Operator (`...`):** Permite "espalhar" todas as propriedades de um objeto como pares chave-valor (atributos) para um elemento JSX.
    
- **Rest Operator (`...rest`):** Em uma desestruturação, coleta todas as propriedades que **não** foram extraídas explicitamente em um novo objeto.
    

Aplicação no Componente List:

Podemos usar o Rest para separar o objectID (que é usado apenas como key na lista) do resto das propriedades do item. Em seguida, usamos o Spread para passar todo o restante para o componente Item.

JavaScript

```
const List = ({ list }) => (
  <ul>
    {list.map(({ objectID, ...item }) => (
      // 1. objectID é extraído para ser usado na key
      // 2. ...item (o resto) é espalhado como props individuais para o componente Item
      <Item key={objectID} {...item} />
    ))}
  </ul>
);
```

Consequentemente, o componente `Item` agora não recebe mais um objeto `item`, mas sim as propriedades individuais (`title`, `url`, etc.) diretamente no primeiro nível das props.

JavaScript

```
const Item = ({ title, url, author, num_comments, points }) => (
  <li>
    <span>
      <a href={url}>{title}</a>
    </span>
    <span>{author}</span>
    <span>{num_comments}</span>
    <span>{points}</span>
  </li>
);
```

Conclusão do Capítulo:

Embora o Spread e Rest sejam poderosos, o livro decide reverter para a implementação mais simples (passando o objeto item explicitamente) para manter o código mais fácil de entender para iniciantes nas próximas seções.

A regra de ouro apresentada é: use a desestruturação de props quase sempre, mas use o _Spread Operator_ apenas quando você estiver apenas repassando props sem precisar acessá-las ou modificá-las 3.

---

Diga **next** para prosseguir para **React Side-Effects**, onde aprenderemos a interagir com o navegador (LocalStorage) usando o hook `useEffect`.