

---

Diretiva é um atributo especial de HTML projetado pelo framework, sendo sempre identificada pelo prefixo estrito v-. O objetivo de uma diretiva é aplicar efeitos colaterais reativos na estrutura do DOM, reagindo no momento em que a variável de estado associada a ela sofre uma mutação.

Uma diretiva é composta por até quatro segmento: `v-on:click.prevent="executarFuncao"`:
- **Argumento (Opcional):** `:` o argumento direciona a ação da diretiva.
- **Modificador (Opcional):**  `.` o modificador atua como uma instrução de alteração de fluxo de execução. `.prevent` aciona o comando `event.preventDefault()` que serve para cancelar o comportamento padrão que o navegador tem ao executar uma ação em um elemento. 
- **Expressão:** valor contido entre as aspas. Consiste na instrução lógica (variável, função ou operação matemática) que será avaliada.

---

**Diretivas Condicionais**
- **v-if:** Se a variável associada for avaliada como verdadeira, o Vue compila e insere o elemento no documento. Se for falsa, remove da árvore de nós.
- **v-else:** Quando o v-if falha, o elemento com v-else é renderizado de forma autônoma.
- **v-show:** O v-show altera exclusivamente a propriedade display, alternando entre none e o valor de exibição padrão do elemento para ocultá-lo ou mostrá-lo visualmente.
	![300](../../attachments/Pasted%20image%2020260823162739.png)
 **Diretiva de Iteração**
- **v-for:** Para cada item presente na estrutura de dados reativa, a diretiva clona o bloco HTML onde foi declarada e injeta os valores locais, automatizando a construção de listas e tabelas.

**Diretivas de Vinculação de Dados**
- **v-bind (ou :):** É utilizada atualizar valores de atributos HTML, como `src` ou `href`.
- **v-model:** Aplicada em elementos de entrada de formulários. Ela injeta o valor da variável no campo e escuta a digitação do usuário para atualizar a variável.
	![400](../../attachments/Pasted%20image%2020260823162951.png)
**Diretiva de Escuta de Eventos**
- **v-on (ou @):** Registra ouvintes de eventos da API nativa do navegador (como `click`, `keyup`, `submit`, `scroll`) no elemento HTML. 
![450](../../attachments/Pasted%20image%2020260823160856.png)![](../../attachments/Pasted%20image%2020260823161949.png)