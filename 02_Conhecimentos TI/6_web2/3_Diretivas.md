

---

Diretiva é um atributo especial de HTML projetado pelo framework, sendo sempre identificada pelo prefixo estrito v-. O objetivo de uma diretiva é aplicar efeitos colaterais reativos na estrutura do DOM, reagindo no momento em que a variável de estado associada a ela sofre uma mutação.

Uma diretiva é composta por até quatro segmento: `v-on:click.prevent="executarFuncao"`:
- **Argumento (Opcional):** Separado por `:`, o argumento direciona a ação da diretiva. O arg `click` informa que deve ser monitrado eventos de clique do mouse.
- **O Modificador (Opcional):** Separado por `.`, o modificador atua como uma instrução de alteração de fluxo de execução. `.prevent` aciona o comando nativo `event.preventDefault()` que serve para cancelar o comportamento padrão que o navegador tem ao executar uma ação em um elemento. 
- **Expressão:** O valor contido entre as aspas. Consiste na instrução lógica (variável, função ou operação matemática) que será avaliada pelo compilador para determinar o valor da operação.

---

**Diretivas Condicionais**
- **v-if:** Se a variável associada for avaliada como verdadeira, o Vue compila e insere o elemento no documento. Se for falsa, remove da árvore de nós.
- **v-else:** Quando o v-if falha, o elemento com v-else é renderizado de forma autônoma.
- **v-show:** O v-show altera exclusivamente a propriedade display, alternando entre none e o valor de exibição padrão do elemento para ocultá-lo ou mostrá-lo visualmente.

 **Diretiva de Iteração**
- **v-for:** Para cada item presente na estrutura de dados reativa, a diretiva clona o bloco HTML onde foi declarada e injeta os valores locais, automatizando a construção de listas e tabelas.

**Diretivas de Vinculação de Dados**
- **v-bind (ou :):** É utilizada para injetar valores de variáveis em atributos HTML nativos, como as propriedades `src` de imagens, `href` de links.
- **v-model:** É aplicada exclusivamente em elementos de entrada de formulários (`<input>`, `<select>`, `<textarea>`). Ela injeta o valor da variável reativa no campo visual e, simultaneamente, escuta a digitação do usuário para atualizar a variável no código.

**Diretiva de Escuta de Eventos**
- **v-on (ou @):** Registra ouvintes de eventos da API nativa do navegador (como `click`, `keyup`, `submit`, `scroll`) no elemento HTML. 
![450](../../attachments/Pasted%20image%2020260823160856.png)