
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
- O nome da função deve obrigatoriams dente começar com letra maiúscula. O React diferencia componentes personalizadoe tags HTML nativas através dessa convenção .
    
**Escopo de Variáveis:** Variáveis podem ser definidas dentro ou fora do componente.    
- _Dentro:_ A variável é redefinida a cada vez que a função do componente é executada.
- _Fora:_ Se a variável não depende de lógica interna, ela pode ser definida fora para evitar redefinição constante.

---
### **2. React JSX**

O retorno da função do componente não é HTML puro, mas sim **JSX (JavaScript XML)**. O JSX é uma extensão de sintaxe que permite misturar HTML e JavaScript. Para renderizar conteúdo dinâmico (variáveis JavaScript) dentro do JSX, utiliza-se a sintaxe de chaves `{}`.

**Atributos HTML no JSX:** Devido ao JSX ser transpilado para JavaScript, algumas palavras reservadas não podem ser usadas como atributos HTML nativos. 

- **`className`:** Substitui o atributo `class` do HTML.
- **`htmlFor`:** Substitui o atributo for usado em labels 

**Transpilar**:  Processo de converter código-fonte de uma linguagem para outra  mantendo um nível de abstração similar. O processo de transpilação (feito pelo Vite) pega esse código JSX e o transforma em JavaScript padrão.

**Interpolação de Dados:** O JSX permite a interpolação de qualquer expressão JavaScript dentro das chaves, não apenas strings primitivas. Isso inclui:

- Propriedades de objetos (ex: `{welcome.text}`).
- Execução de funções (ex: `{getTitle('React')}`).
