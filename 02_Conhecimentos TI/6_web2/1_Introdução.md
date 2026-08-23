


---

Criando projeto VUE: `npm init vue@latest`
![](../../attachments/Pasted%20image%2020260823134042.png)
- **Vitest**: Adiciona o framework Vitest para a criação de testes unitários. 
- **End-to-End Testing**: Configura ferramentas para testes de ponta a ponta. Testes E2E automatizam um navegador real para simular ações de um usuário completo no sistema.
- **Linter**: Ferramenta que inspeciona seus arquivos em busca de erros de sintaxe, variáveis não utilizadas ou violações de boas práticas antes mesmo da aplicação ser executada. 
- **Prettier**: Stua em conjunto com o Linter para padronizar o estilo visual do seu código-fonte, aplicando regras consistentes de indentação, espaçamentos e uso de aspas simples ou duplas.

- **npm install**: Lê as especificações do arquivo `package.json` e realiza o download de todas as dependências necessárias para o funcionamento do projeto.
- **npm run format**: aiona o Prettier para analisar o código e aplicar as regras de formatação.
- **npm run dev**: Inicia o servidor de desenvolvimento local utilizando o Vite. 

Após dar uma limpada no projeto: Note que é possível esconder visualmente arquivos de config em .vscode/settings.json em fikes.ex
![](../../attachments/Pasted%20image%2020260823140933.png)
**index.html**: Único arquivo HTML estático da aplicação. Fornece um contêiner vazio na árvore de elementos onde a interface gerada por JavaScript será inserida.
- A div id app é o alvo de montagem.
- A tag script instrui o navegador a carregar o código fonte principal.    ![550](../../attachments/Pasted%20image%2020260823140410.png)
**main.ts**: Ponto de inicialização do sistema. É aqui que o motor do Vue é instanciado e as configurações globais são definidas.
- **createApp(App):** gera a instância principal da sua aplicação em memória.
- **mount:** é a ponte entre o Vue e o HTML. Instrui a instância criada a processar todo o código Vue e renderizar o resultado visual final substituindo a `<div id="app"></div>` ![300](../../attachments/Pasted%20image%2020260823140619.png)
**App.vue**: O Vue utiliza o conceito de _Single-File Components_ (SFC), que encapsula a lógica, a estrutura visual e o estilo de uma parte da interface em um único arquivo com a extensão `.vue`. O `App.vue` é o nó principal (pai) de toda a árvore de componentes da sua aplicação.

  

Um arquivo `.vue` moderno é subdividido em três blocos estritos:

  

- **`<script setup lang="ts">`:** Armazena a lógica de negócios, variáveis de estado e funções em TypeScript. O atributo `setup` indica que a aplicação está utilizando a _Composition API_, o modelo arquitetural mais recente do Vue para gerenciamento de reatividade.
    
      
    
- **`<template>`:** Contém a estrutura da interface do usuário. É aqui que você escreve o HTML enriquecido com diretivas próprias do Vue (como laços de repetição ou renderizações condicionais).
    
      
    
- **`<style scoped>`:** Define a formatação CSS. O atributo opcional `scoped` garante que as regras de estilo definidas aqui sejam aplicadas exclusivamente a este componente, prevenindo vazamento de formatação para outras áreas do sistema.
    
      
    
- **Link oficial:** [https://vuejs.org/guide/essentials/component-basics.html](https://vuejs.org/guide/essentials/component-basics.html)
    
      
    

### Onde focar os estudos a seguir

Com o arquivo raiz limpo, o desenvolvimento consistirá em criar pequenos arquivos independentes dentro da pasta `src/components` (como botões, cabeçalhos ou formulários) e importá-los para dentro do bloco `<template>` do `App.vue`.

  

Para conseguir construir esses primeiros componentes, os três próximos tópicos de estudo na documentação devem ser:

  

1. **Reatividade:** Como declarar variáveis que atualizam a tela automaticamente quando seus valores mudam (funções `ref` e `reactive`).
    
      
    
2. **Diretivas de Template:** Como utilizar estruturas condicionais (`v-if`) e laços de repetição (`v-for`) diretamente no HTML.
    
      
    
3. **Eventos:** Como capturar cliques de usuários e interações (`v-on` ou o atalho `@`).