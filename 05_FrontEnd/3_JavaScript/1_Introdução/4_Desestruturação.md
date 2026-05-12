
 #Concluded  

---
### **1. Arrays**
Os arrays em js podem ter qualquer tipo de dado
![Pasted image 20250513162620](../../../attachments/Pasted%20image%2020250513162620.png)

### **2. Desestruturação**
A desestruturação é um recurso que permite extrair dados específicos de propriedades de objetos ou elementos de arrays, atribuindo-os diretamente a variáveis individuais em uma única instrução.

Exemplo com objeto e array
```js
// Exemplo com Objeto
const book = {
  title: "The Fellowship of the Ring",
  author: "J.R.R. Tolkien",
  pages: 423
};

const { title, author } = book;
console.log(title); 

// Exemplo com Array
const genres = ["Fantasy", "Adventure", "Action", "Drama"];

const [primaryGenre, secondaryGenre] = genres;
console.log(primaryGenre);
```

**Rest Operator**: O operador rest, representado por três pontos (`...`), atua em conjunto com a desestruturação. Sua finalidade é coletar e agrupar todos os elementos ou propriedades restantes que não foram explicitamente extraídos.

O operador _rest_ deve ser obrigatoriamente o último elemento na declaração de desestruturação, caso contrário, ocorrerá um erro de sintaxe.
```js
const genres = ["Fantasy", "Adventure", "Action", "Drama", "Magic"];

// Extraindo os dois primeiros e agrupando o restante em um novo array
const [primaryGenre, secondaryGenre, ...otherGenres] = genres;

console.log(primaryGenre); // Saída: Fantasy
console.log(otherGenres);  // Saída: ["Action", "Drama", "Magic"]
```

**Spread Operator**: Embora utilize a mesma sintaxe de três pontos (`...`), o operador _spread_ executa a operação inversa ao _rest_: ele espalha os elementos de uma estrutura iterável para dentro de uma nova estrutura. 

- **Uso em Arrays:** Permite combinar arrays ou adicionar novos elementos no início ou no final de uma nova lista, mantendo os dados originais intactos.
```js
const currentGenres = ["Fantasy", "Adventure"];

// Expandindo o array original e adicionando um novo elemento no final
const newGenres = [...currentGenres, "Epic Fantasy"];
```

- **Uso em Objetos:** Permite criar um novo objeto contendo todas as propriedades do objeto original. Além disso, possibilita a inserção de novas propriedades ou a sobrescrita (atualização) de propriedades existentes. 
```js
const originalBook = {
  title: "The Fellowship of the Ring",
  pages: 423,
  publicationYear: 1954
};

// Expandindo o objeto
const updatedBook = {
  ...originalBook,
  moviePublicationDate: "2001-12-19", // Adicionando nova propriedade
  pages: 432 // Sobrescrevendo a propriedade existente 'pages'
};
```
