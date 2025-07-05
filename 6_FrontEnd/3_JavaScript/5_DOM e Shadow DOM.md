
---

### **1. O DOM (Document Object Model)**
DOM é o "mapa vivo" de toda a sua página HTML. 
- Qualquer script na sua página pode, por padrão, acessar e manipular qualquer elemento no DOM usando `document.querySelector()` ou `getElementById()`.
- Uma regra de estilo definida no seu arquivo CSS (ou numa tag `<style>`), como `p { color: blue; }`, vai se aplicar a **todos** os parágrafos `<p>` da página inteira. Não há barreiras.
- Existe apenas um DOM principal por página.

**Na prática:** É ótimo para a estrutura geral da página, mas em aplicações grandes, essa natureza global pode causar problemas. 

---
### **2. O Shadow DOM**
O **Shadow DOM** resolve os problemas de vazamento do DOM principal. Ele permite que um elemento HTML (chamado de "host") tenha sua própria "árvore DOM" particular e encapsulada.

Pense no Shadow DOM como um **quarto privado dentro da casa**.

- **É Encapsulado (Seu Superpoder):** O que acontece no Shadow DOM, fica no Shadow DOM.
    
    - **CSS com Escopo Definido:** Estilos definidos dentro do Shadow DOM se aplicam **apenas** aos elementos dentro dele. Eles não vazam para o resto da página. Da mesma forma, os estilos globais da página **não entram** no Shadow DOM (com algumas exceções controladas).
        
    - **JavaScript Protegido:** `document.querySelector()` executado na página principal **não pode** encontrar elementos dentro de um Shadow DOM. O JavaScript de fora não consegue acessar e modificar acidentalmente a estrutura interna do componente.
        
- **Composição:** Ele não substitui o DOM principal, mas vive "anexado" a um elemento dele. O elemento que hospeda o Shadow DOM é chamado de **Shadow Host**. A raiz da árvore privada é chamada de **Shadow Root**.
    

**Por que usar?** Para criar **componentes reutilizáveis e autossuficientes**. Imagine criar um `<video-player>` customizado. Você quer que os botões de "play", a barra de progresso e os estilos dele funcionem de forma independente, não importa onde você o coloque na sua aplicação, sem risco de conflito com outros CSS ou JS da página.
### 1. A Analogia: O DOM é o "Mapa Vivo" da sua Página

Imagine seu arquivo HTML como a planta de uma casa. O navegador lê essa planta e constrói a casa de verdade. O **DOM (Document Object Model)** é como um "mapa vivo" e interativo dessa casa já construída.

Com JavaScript, você não edita a planta original (o arquivo `.html`), mas sim usa esse mapa vivo (o DOM) para interagir com a casa: você pode pintar uma parede, abrir uma porta, adicionar um móvel novo ou até demolir um cômodo. Tudo isso em tempo real, sem precisar recarregar a página.

O DOM organiza a página em uma estrutura de árvore de "nós" (nodes). O `<html>` é o nó raiz, o `<head>` e o `<body>` são seus filhos, e assim por diante.

![600](../../attachments/Pasted%20image%2020250705152711.png)

---

### 2. O Projeto Prático: Uma Lista de Tarefas Simples

Vamos criar uma página simples onde podemos adicionar e remover tarefas.

**Nosso HTML Base (`index.html`):**

Crie um arquivo com este conteúdo. Ele será a "planta" da nossa casa.

HTML

```
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <title>DOM na Prática</title>
    <style>
        body { font-family: sans-serif; background-color: #f4f4f4; padding: 20px; }
        #container { max-width: 500px; margin: auto; background: white; padding: 20px; border-radius: 8px; }
        h1 { color: #333; }
        input { width: 70%; padding: 8px; }
        button { padding: 8px; cursor: pointer; }
        ul { list-style-type: none; padding: 0; }
        li { padding: 10px; border-bottom: 1px solid #ddd; display: flex; justify-content: space-between; align-items: center; }
        li button { background-color: #e74c3c; color: white; border: none; }
    </style>
</head>
<body>

    <div id="container">
        <h1>Minha Lista de Tarefas</h1>
        
        <input type="text" id="nova-tarefa-input" placeholder="O que precisa ser feito?">
        <button id="adicionar-tarefa-btn">Adicionar</button>

        <h2>Tarefas a Fazer</h2>
        <ul id="lista-de-tarefas">
            </ul>
    </div>

    <script src="script.js"></script>

</body>
</html>
```

Agora, vamos criar o arquivo `script.js`. É aqui que a mágica acontece.

### 3. JavaScript em Ação (no arquivo `script.js`)

O processo de manipulação do DOM quase sempre segue 3 passos:

1. **Selecionar** o(s) elemento(s) que você quer manipular.
    
2. **Manipular** o elemento (mudar seu estilo, texto, etc.) ou **escutar** um evento (como um clique).
    
3. **Adicionar ou Remover** elementos da página, se necessário.
    

#### Passo 1: Selecionar os Elementos Principais

Primeiro, precisamos de referências aos elementos do HTML com os quais vamos interagir.

JavaScript

```
// script.js

// Seleciona o botão de adicionar pelo seu ID
const botaoAdicionar = document.getElementById('adicionar-tarefa-btn');

// Seleciona o campo de input pelo seu ID
const inputTarefa = document.getElementById('nova-tarefa-input');

// Seleciona a lista (<ul>) onde as tarefas serão adicionadas
const listaDeTarefas = document.getElementById('lista-de-tarefas');
```

- `document.getElementById()`: É a forma mais rápida de pegar um elemento que possui um `id` único.
    

#### Passo 2: Responder a um Evento (O Clique do Botão)

Queremos que algo aconteça quando o usuário clicar no botão "Adicionar". Para isso, usamos um "ouvinte de evento" (`EventListener`).

JavaScript

```
// Adiciona um "ouvinte" para o evento de 'click' no botão
botaoAdicionar.addEventListener('click', function() {
    // Esta função será executada toda vez que o botão for clicado
    
    // Pega o texto que o usuário digitou no input
    const textoDaTarefa = inputTarefa.value;

    // Verifica se o usuário realmente digitou algo
    if (textoDaTarefa.trim() === '') {
        alert('Por favor, digite uma tarefa.');
        return; // Para a execução se nada foi digitado
    }
    
    // Agora, vamos criar e adicionar a nova tarefa na tela
    adicionarNovaTarefa(textoDaTarefa);

    // Limpa o campo de input para a próxima tarefa
    inputTarefa.value = '';
    
    // Devolve o foco para o campo de input
    inputTarefa.focus();
});
```

#### Passo 3: Criar, Manipular e Adicionar Novos Elementos

A função `adicionarNovaTarefa` é onde realmente modificamos a estrutura da página.

JavaScript

```
function adicionarNovaTarefa(texto) {
    // 1. CRIAR os novos elementos HTML
    const novoItemLi = document.createElement('li'); // Cria um <li></li>
    const textoLi = document.createTextNode(texto); // Cria um nó de texto com o que o usuário digitou
    const botaoRemover = document.createElement('button'); // Cria um <button></button>

    // 2. MANIPULAR os elementos criados
    botaoRemover.textContent = 'Remover'; // Define o texto do botão

    // Adiciona um evento de clique no botão de remover que acabamos de criar
    botaoRemover.addEventListener('click', function() {
        // 'this' se refere ao botão que foi clicado
        // '.parentElement' se refere ao pai do botão, que é o <li>
        this.parentElement.remove(); // O método .remove() é a forma moderna de deletar um elemento
    });
    
    // 3. MONTAR a estrutura e ADICIONAR à página
    novoItemLi.appendChild(textoLi); // Coloca o texto dentro do <li>  --> <li>Texto da Tarefa</li>
    novoItemLi.appendChild(botaoRemover); // Coloca o botão dentro do <li> --> <li>Texto da Tarefa<button>Remover</button></li>

    // Finalmente, adiciona o novo <li> completo dentro da nossa lista <ul>
    listaDeTarefas.appendChild(novoItemLi);
}
```

### Resumo do que fizemos na prática:

1. **`document.getElementById()`**: Selecionamos os "atores" principais da nossa página (input, botão e lista).
    
2. **`addEventListener()`**: Ensinamos o botão a "ouvir" por cliques e executar uma ação específica.
    
3. **`.value`**: Lemos o conteúdo de um campo de `input`.
    
4. **`document.createElement()`**: Criamos novos elementos (`li`, `button`) que não existiam no HTML original.
    
5. **`.textContent`**: Definimos o texto visível de um elemento.
    
6. **`appendChild()`**: Anexamos um elemento filho dentro de um elemento pai, efetivamente "desenhando" na tela.
    
7. **`.remove()`**: Deletamos um elemento da página de forma interativa.
    

Abra o arquivo `index.html` no seu navegador e você terá uma aplicação funcional, toda manipulada via JavaScript através do DOM!


![Pasted image 20250527105708](../../attachments/Pasted%20image%2020250527105708.png)
