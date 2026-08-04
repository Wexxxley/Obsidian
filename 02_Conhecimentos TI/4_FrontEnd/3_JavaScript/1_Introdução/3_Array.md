

---
Os arrays em js podem ter qualquer tipo de dado
![Pasted image 20250513162620](../../../../attachments/Pasted%20image%2020250513162620.png)
#### **1. map**
Este método itera sobre todos os elementos do array original e executa uma função _callback_ para cada um deles. O resultado é armazenado em um novo array, que é retornado ao final do processo. 
```js
const numeros = [1, 2, 3, 4];
const numerosDobrados = numeros.map(numero => numero * 2);
console.log(numerosDobrados); // Saída: [2, 4, 6, 8]
console.log(numeros);         // Saída: [1, 2, 3, 4] (Intacto)
```
#### **2. reduce**
Utilizado para reduzir um array a um único valor. O método executa uma função _callback_ em cada elemento do array, passando o valor de retorno do cálculo do elemento anterior para o próximo.
```js
const valores = [10, 20, 30, 40];

// 'acumulador' guarda a soma, 'valorAtual' é o item da iteração
const somaTotal = valores.reduce((acumulador, valorAtual) => {
  return acumulador + valorAtual;
}, 0); // 0 é o valor inicial do acumulador
```
#### **3. Filter**
Cria um novo array contendo apenas os elementos do array original que passarem em um teste lógico especificado pela função _callback_.
```js
const idades = [15, 22, 17, 30, 12, 18];
// Filtra apenas valores maiores ou iguais a 18
const maioresDeIdade = idades.filter(idade => idade >= 18);
console.log(maioresDeIdade); // Saída: [22, 30, 18]
```
#### **4. find**
Retorna o valor do primeiro elemento no array que satisfizer a função de teste provida. Caso nenhum elemento atenda à condição, o retorno será undefined.
```js
const usuarios = [{ id: 1, nome: "Carlos" },{ id: 2, nome: "Ana" },];
// Busca o objeto cujo id seja estritamente igual a 2
const usuarioEncontrado = usuarios.find(usuario => usuario.id === 2);
```
#### **5. includes**
Ele determina se um array contém um determinado elemento, retornando `true` ou `false` 
```js
const linguagens = ["JavaScript", "Python", "C#", "Java"];
const possuiCSharp = linguagens.includes("C#");
```
### 6. some e every
```js
const notas = [7, 8, 5, 9, 10];

// Verifica se existe alguma nota menor que 6
const temReprovado = notas.some(nota => nota < 6);
console.log(temReprovado); // Saída: true

// Verifica se todas as notas são maiores ou iguais a 5
const todosPassaramMinimo = notas.every(nota => nota >= 5);
console.log(todosPassaramMinimo); // Saída: true
```
#### **7. forEach**
Executa uma função fornecida uma vez para cada elemento do array. Este método não retorna um novo array e é tipicamente utilizado quando o objetivo é causar efeitos colaterais, como registrar dados no console ou atualizar variáveis externas.
```js
const nomes = ["Alice", "Bob", "Charlie"];
nomes.forEach((nome, indice) => {
  console.log(`Posição ${indice}: ${nome}`);
});
```

#### **8. sort**
Ordena os elementos de um array e retorna a referência para o mesmo array. É necessário fornecer uma função de comparação.
```js
const numerosDesordenados = [40, 1, 5, 200];
// Ordenação numérica ascendente
numerosDesordenados.sort((a, b) => a - b);
console.log(numerosDesordenados); // Saída: [1, 5, 40, 200]
```