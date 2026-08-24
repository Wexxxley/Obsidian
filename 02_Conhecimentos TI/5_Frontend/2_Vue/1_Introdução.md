
#Concluded 

---
### 1. Arquitetura MVVM
![500](../../../attachments/Pasted%20image%2020260823144610.png)
**Model**: Esta camada representa as regras de negócio puras, o formato dos dados em memória e a comunicação com fontes de informação externas.
**View**: A View é a camada de apresentação visual, responsável estritamente por desenhar elementos na tela. A regra da View na arquitetura MVVM é a ausência de lógica de negócios.
**ViewModel**: Atua como um adaptador de estado, importando os dados brutos do Model, convertendo-os para um formato adequado para a interface e os armazenando em variáveis de estado. No Vue, é encapsulado por todo o código em TS escrito dentro da tag `<script setup>`.

**Data Binding**: A View e o ViewModel são conectados por um sistema de rastreamento de dependências contínuo, sem a necessidade de comandos manuais de manipulação.
- **Delegação de Eventos:** Quando o usuário realiza uma ação na View, ela emite o evento para o ViewModel através de gatilhos definidos na interface.
- **Mutação de Estado:** O ViewModel recebe a chamada, executa o processamento algorítmico e altera o valor de suas variáveis internas em memória.
- **Atualização Autônoma:** Como as variáveis são declaradas como entidades reativas, o framework detecta a mutação. motor de renderização, então, atualiza a View, redesenhando apenas os componentes estritamente dependentes daquele novo valor.

---
### 2. iniciando um projeto VUE

Criando projeto VUE: `npm init vue@latest`
![](../../../attachments/Pasted%20image%2020260823134042.png)
- **Vitest**: Adiciona o framework Vitest para a criação de testes unitários. 
- **End-to-End Testing**: Configura ferramentas para testes de ponta a ponta. Testes E2E automatizam um navegador real para simular ações de um usuário completo no sistema.
- **Linter**: Ferramenta que inspeciona seus arquivos em busca de erros de sintaxe, variáveis não utilizadas ou violações de boas práticas antes mesmo da aplicação ser executada. 
- **Prettier**: Stua em conjunto com o Linter para padronizar o estilo visual do seu código-fonte, aplicando regras consistentes de indentação, espaçamentos e uso de aspas simples ou duplas.

- **npm install**: Lê as especificações do arquivo `package.json` e realiza o download de todas as dependências necessárias para o funcionamento do projeto.
- **npm run format**: aiona o Prettier para analisar o código e aplicar as regras de formatação.
- **npm run dev**: Inicia o servidor de desenvolvimento local utilizando o Vite. 

Após dar uma limpada no projeto: Note que é possível esconder visualmente arquivos de config em .vscode/settings.json em fikes.exclude. ![](../../../attachments/Pasted%20image%2020260823141105.png)
**index.html**: Único arquivo HTML estático da aplicação. Fornece um contêiner vazio na árvore de elementos onde a interface gerada por JavaScript será inserida.
- A div id app é o alvo de montagem.
- A tag script instrui o navegador a carregar o código fonte principal.    ![550](../../../attachments/Pasted%20image%2020260823140410.png)
**main.ts**: Ponto de inicialização do sistema. É aqui que o motor do Vue é instanciado e as configurações globais são definidas.
- **createApp(App):** gera a instância principal da sua aplicação em memória.
- **mount:** é a ponte entre o Vue e o HTML. Instrui a instância criada a processar todo o código Vue e renderizar o resultado visual final substituindo a `<div id="app"></div>` ![300](../../../attachments/Pasted%20image%2020260823140619.png)
**App.vue**:  É o nó principal (pai) de toda a árvore de componentes da sua aplicação. Um arquivo .vue é subdividido em três blocos:
![](../../../attachments/Pasted%20image%2020260823141416.png)
-  O atributo opcional scoped garante que as regras de estilo definidas aqui sejam aplicadas exclusivamente a este componente.
