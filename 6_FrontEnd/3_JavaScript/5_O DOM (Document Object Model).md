
---
### **1. O DOM (Document Object Model)**
DOM é uma árvore de toda a sua página HTML. 
- **Qualquer script** na sua página pode **acessar e manipular** qualquer elemento no DOM usando `document.querySelector()` ou `getElementById()`.
- Uma regra de estilo definida no seu arquivo CSS vai se aplicar a **todos** os elementos da página 
- Existe apenas um DOM principal por página.
![550](../../attachments/Pasted%20image%2020250705152711.png)

---
### **2. O Projeto Prático: Uma Lista de Tarefas Simples**

![](../../attachments/Pasted%20image%2020250705154046.png)
O processo de manipulação do DOM quase sempre segue 3 passos:
1. **Selecionar** o elemento que você quer manipular.
2. **Manipular** o elemento ou **escutar** um evento (como um clique).
3. **Adicionar ou Remover** elementos da página.
#### **2.1 Selecionar elementos 
![](../../attachments/Pasted%20image%2020250705154818.png)
- `document.getElementById()`: Forma mais rápida de pegar um elemento que possui um `id`.
#### **2.2: Responder a um Evento**
Queremos que algo aconteça quando o usuário clicar no botão "Adicionar". Para isso, usamos um "ouvinte de evento" (`EventListener`).
![](../../attachments/Pasted%20image%2020250705154907.png)

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


![](../../attachments/Pasted%20image%2020250705153959.png)