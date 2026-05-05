
#Concluded 

---
**Dialog**: É uma janela flutuante que é renderizada sobreposta ao conteúdo principal.
- **Renderização Condicional:** a instanciação é controlada por uma instrução if. Quando a variável de estado se torna verdadeira, o bloco de código é alcançado e o Dialog é adicionado à árvore de renderização.
- **onDismissRequest:** É um parâmetro obrigatório que atua como um callback. O sistema operacional o invoca quando detecta que o usuário deseja fechar o diálogo (geralmente tocando fora da área visível.
- **DialogProperties:** Uma classe que permite configurar o comportamento da janela do diálogo junto ao sistema operacional.
- **Surface**: Dialog nativo não possui cor de fundo, bordas arredondadas ou sombra. O componente Surface é utilizado para materializar a interface gráfica. Ele aplica a cor de fundo padrão.

**ProgressIndicator**: Existem fundamentalmente dois tipos de indicadores de progresso nativos: o formato circular e o formato linear. Cada um deles pode operar em dois modos distintos: determinado e indeterminado.
- **Modo Indeterminado:** Invocado quando o componente não recebe o parâmetro de progresso. 
- **Modo Determinado:** Invocado quando a propriedade progress recebe uma função lambda ou um valor Float. O valor deve estar no intervalo 0.0f - 1.0f     

![620](../../../attachments/Pasted%20image%2020260428085802.png)
![](../../../attachments/Pasted%20image%2020260428085833.png)
![200](../../../attachments/Peek%202026-04-28%2008-52.gif)
