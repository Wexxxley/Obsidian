

---
### **1. Single-Page Applications (SPA)**
 
Em uma arquitetura tradicional (**Server-Side Rendering**), o navegador recebe um documento HTML pronto, onde a estrutura visual já está escrita. Em uma SPA com React, o processo é invertido:

1. O servidor envia um arquivo HTML quase vazio.

2. O navegador baixa e executa o pacote JavaScript (seu código React). O React não "lê" o HTML; ele gera o HTML. O código JavaScript executa lógica para criar elementos DOM (como `<h1>`, `<div>`) e injetá-los dinamicamente dentro da `div` raiz vazia.

---
### **2. Inicialização do Projeto com Vite**

Para o desenvolvimento moderno em React, o ambiente requer: **Node.js e NPM**, necessários para gerenciar bibliotecas e dependências (pacotes Node) que o projeto utilizará. O NPM (Node Package Manager) permite a instalação via linha de comando.

O **Vite** é uma ferramenta de build, substituindo configurações manuais complexas. O Vite consiste em dois componentes principais:

```a
npm create vite@latest hacker-stories -- --template react
```

Após a criação, as dependências listadas no `package.json` são instaladas via `npm install` e o servidor é iniciado com `npm run dev` .

#### 4. Estrutura de Arquivos e Scripts (Páginas 18 a 21)

Ao abrir o projeto, a estrutura de diretórios revela a arquitetura técnica da aplicação:

- **`package.json`:** Manifesto do projeto que lista dependências e scripts de configuração.
    
- **`vite.config.js`:** Arquivo de configuração do Vite, onde plugins (como o plugin do React) são definidos.
    
- **`index.html`:** O ponto de entrada no navegador. Ele contém um elemento `div` (geralmente com `id="root"`) e uma tag `<script>` que aponta para o código fonte (`src/main.jsx`) . O React injetará a aplicação dentro deste `div`.
    
- **`src/`:** Diretório contendo o código-fonte da aplicação.
    
    - **`src/main.jsx`:** O ponto de entrada JavaScript (entry point).
        
    - **`src/App.jsx`:** Onde o componente raiz da aplicação é implementado.
        

**Scripts NPM (Página 15/20):** Os scripts definidos no `package.json` automatizam tarefas:

- `npm run dev`: Inicia o servidor de desenvolvimento.
    
- `npm run build`: Compila a aplicação para a pasta `dist/`, pronta para produção.
    
- `npm run preview`: Simula o ambiente de produção localmente após o build.