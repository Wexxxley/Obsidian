
#Concluded 

---
### **1. Componente**

Toda aplicação React é construída sobre **componentes**. O ponto de partida é o arquivo `src/App.jsx`. Para simplificar, é melhor fazer a substituição do conteúdo de `src/App.jsx` por uma versão minimalista:
```jsx
import * as React from 'react';

const title = 'React';

function App() {
  return (
    <div>
      <h1>Hello {title}</h1>
    </div>
  );
}

export default App;
```
- O componente `App` é declarado como uma função JavaScript.  
- O nome da função deve obrigatoriams dente começar com letra maiúscula. <mark style="background: #ADCCFFA6;">O React diferencia componentes personalizado e tags HTML nativas através dessa convenção</mark>.

---
### **2. JSX (JavaScript XML)**

O retorno do componente não é HTML puro, mas sim **JSX (JavaScript XML)**. O JSX é uma extensão de sintaxe que <mark style="background: #ADCCFFA6;">permite misturar HTML e JavaScript. Para renderizar conteúdo dinâmico dentro do JSX</mark>, utiliza-se a sintaxe de chaves `{}`.

Devido ao JSX ser transpilado para JavaScript, algumas palavras reservadas não podem ser usadas como atributos HTML nativos. 

- **`className`:** Substitui o atributo `class` do HTML.
- **`htmlFor`:** Substitui o atributo for usado em labels 

**Transpilar**: <mark style="background: #ADCCFFA6;"> Processo de converter código-fonte de uma linguagem para outra  mantendo um nível de abstração similar.</mark> O processo de transpilação (feito pelo Vite) pega esse código JSX e o transforma em JavaScript padrão.

---
### **3. Listando itens**

O método map() de arrays é o padrão para iterar sobre dados e retornar elementos JSX. Inicialmente, vamos definir uma lista fora do componente, simulando dados de uma API.
![](../../attachments/Pasted%20image%2020251123171205.png)

Dentro do JSX, utiliza-se chaves {} para executar o código JavaScript. 
![](../../attachments/Pasted%20image%2020251123171325.png)

O React <mark style="background: #ADCCFFA6;">exige que cada elemento renderizado via iteração de array possua um atributo key</mark>. O key é um identificador que permite o React rastrear quais itens mudaram. O uso do índice do array é desencorajado, pois a reordenação da lista pode causar bugs de estado no componente.
