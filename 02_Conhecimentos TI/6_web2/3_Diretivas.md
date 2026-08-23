

---

Diretiva é um atributo especial de HTML projetado pelo framework, sendo sempre identificada pelo prefixo estrito v-. O objetivo de uma diretiva é aplicar efeitos colaterais reativos na estrutura do DOM, reagindo no momento em que a variável de estado associada a ela sofre uma mutação.

Uma diretiva é composta por até quatro segmento: `v-on:click.prevent="executarFuncao"`:
- **Argumento (Opcional):** Separado por `:`, o argumento direciona a ação da diretiva. O arg `click` informa que deve ser monitrado eventos de clique do mouse.
- **O Modificador (Opcional):** Separado por `.`, o modificador atua como uma instrução de alteração de fluxo de execução. `.prevent` aciona o comando nativo `event.preventDefault()` que serve para cancelar o comportamento padrão que o navegador tem ao executar uma ação em um elemento. 
- **Expressão:** O valor contido entre as aspas. Consiste na instrução lógica (variável, função ou operação matemática) que será avaliada pelo compilador para determinar o valor da operação.

- **Manipulação Estrutural de Nós:** Diretivas como `v-if`, `v-else`, `v-show` e `v-for` controlam a renderização condicional, alterando fisicamente a presença, destruição ou a repetição de elementos na árvore do DOM.
    
      
    
- **Sincronização de Estado:** Diretivas como `v-bind` (para a injeção unilateral de variáveis em atributos HTML) e `v-model` (para o mapeamento bidirecional de dados em campos de formulários).
    
      
    
- **Interceptação de Eventos:** A diretiva `v-on` atua na camada de interação, registrando ouvintes para processar entradas do usuário.