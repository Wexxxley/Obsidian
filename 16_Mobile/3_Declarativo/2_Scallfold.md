
#Concluded 

---

Pense no componente scallfold como a estruturação da sua tela. Ele calcula os espaços automaticamente. Por exemplo, se você colocar uma TopBar, o Scaffold empurra o seu texto um pouco para baixo.

O scallfold aceita vários composables como parâmetros: 
- topBar
- bottomBar
- floatingActionButton.

![250](../../attachments/Pasted%20image%2020260318084224.png)

![550](../../attachments/Pasted%20image%2020260318084306.png)
![450](../../attachments/Pasted%20image%2020260318084334.png)

1. **innerPadding**: O scalfold calcula o tamanho da sua `TopAppBar` e da sua `BottomAppBar` e te entrega esse valor através da variável `innerPadding`.
2. **Column**: Organiza o conteudo em coluna.

Depois de criado a função composable, basta iserir no setContent.
![400](../../attachments/Pasted%20image%2020260318084245.png)
