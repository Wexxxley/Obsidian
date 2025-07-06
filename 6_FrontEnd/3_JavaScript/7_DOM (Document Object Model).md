
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

#### **2.3 Criar, Manipular e Adicionar Novos Elementos**

![](../../attachments/Pasted%20image%2020250705155801.png)

1. **`document.getElementById()`**: Selecionamos elentos por id.
2. **`addEventListener()`**: Faz algo quando um evento é acionado.
3. **`.value`**: ler o conteúdo de um campo de `input`.
4. **`document.createElement()`**: Criamos novos elementos
5. **`.textContent`**: Definimos o texto visível de um elemento.
6. **`appendChild()`**: Anexamos um elemento filho dentro de um elemento pai.
7. **`.remove()`**: Deletamos um elemento da página de forma interativa.

![](../../attachments/Pasted%20image%2020250705153959.png)

