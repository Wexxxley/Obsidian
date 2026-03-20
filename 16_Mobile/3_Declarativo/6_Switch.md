

---

O Switch é um componente de seleção binária que oferece duas opções ao usuário: On e Off. Ele é composto fundamentalmente por dois parâmetros obrigatórios:
- **checked:** Um booleano que define o estado visual atual do componente na interface.
- **onCheckedChange:** Uma função de retorno (callback) que é disparada quando o usuário interage com o interruptor, devolvendo o novo valor booleano.

Para que o switch funcione dinamicamente, é necessário criar uma variável de estado 



O instrutor apresenta duas abordagens técnicas para lidar com a visibilidade de elementos (neste caso, uma imagem) baseada no estado do `Switch`:

- **Remoção Condicional (If-Else):** * O componente é inserido dentro de um bloco `if`. Se a condição for falsa, o componente é removido da árvore de UI.
    
    - **Problema:** Quando o componente é removido, os elementos abaixo dele (como um texto) "sobem" para ocupar o espaço vazio, alterando o layout.
        
    - **Solução:** Adicionar um `Spacer` com o mesmo tamanho da imagem no bloco `else` para preservar o espaço ocupado.
        
- **Propriedade Alpha (Recomendado para Animações):**
    
    - Em vez de remover o componente, utiliza-se o modificador `Modifier.alpha(valor)`.
        
    - O valor varia de **1.0f** (totalmente visível) a **0.0f** (totalmente invisível).
        
    - **Vantagem:** O componente continua existindo no layout e ocupando seu espaço original, evitando que outros elementos se desloquem na tela.
        

## 5. Alteração Dinâmica de Texto

Além da imagem, a aula mostra como alterar o conteúdo de um componente `Text` baseando-se no estado do `Switch`. Isso é feito atualizando uma variável de estado de string dentro da lógica do `onCheckedChange` ou através de uma verificação condicional direta na propriedade `text` do componente.

## 6. Organização de Layout

O exemplo utiliza uma `Column` como contêiner principal com as seguintes propriedades:

- `Modifier.fillMaxSize()` para ocupar toda a tela.
    
- `horizontalAlignment = Alignment.CenterHorizontally` para centralizar os elementos.
    
- `Spacer` entre os componentes para gerenciar o respiro visual (margens).
    

Deseja que eu elabore um código de exemplo unificando essas duas formas de controlar a visibilidade mencionadas na aula?