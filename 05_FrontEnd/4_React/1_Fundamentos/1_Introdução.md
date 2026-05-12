
#Concluded 

---
### **1. Inicialização do Projeto com Vite**

Para o desenvolvimento moderno em React, o ambiente requer: **Node.js e NPM**, necessários para gerenciar bibliotecas e dependências. 

O **Vite** é a <mark style="background: #ADCCFFA6;">ferramenta de build</mark> que orquestrar o ambiente de desenvolvimento. 
```
npm create vite@latest nomeProj -- --template react
```

```
cd nomeProj
npm install
npm run dev
```

---
### **3. Análise da Estrutura de Arquivos**

![](../../../attachments/Pasted%20image%2020251123163549.png)

- **index.htm:** Este é o arquivo que o navegador carrega primeiro. Ele contém uma tag src que instrui o navegador a carregar o ponto de entrada js.
	![](../../../attachments/Pasted%20image%2020251123163711.png)
        
- **src/main.jsx:** Arquivo é responsável por inicializar a árvore de componentes do React e anexá-la ao elemento root definido no HTML.
    ![](../../../attachments/Pasted%20image%2020251123163935.png)
    
- **src/App.jsx:** Contém a definição do componente raiz. É aqui que a lógica da aplicação começa a ser implementada.
    ![](../../../attachments/Pasted%20image%2020251123164023.png)
    
- **package.json:** O arquivo que define as dependências e os metadados do projeto.
        
- **vite.config.js:** Arquivo de configuração do Vite. Nele, o plugin do React é ativado para permitir que o Vite entenda e transpile a sintaxe JSX.
	![](../../../attachments/Pasted%20image%2020251123164152.png)

---
### **4. Scripts de Automação** 

O package.json define scripts que abstraem comandos complexos do Vite.

- **npm run dev:** Inicia o servidor de desenvolvimento local. Ele suporta Hot Module Replacement.
- **npm run build:** Compila a aplicação para produção. Cria a pasta dist/ com arquivos HTML/CSS/JS prontos para deploy.
- **npm run preview:** Serve localmente os arquivos da pasta dist/ para testar como a aplicação se comportará em produção.

