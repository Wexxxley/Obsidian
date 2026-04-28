
#Concluded 

---
Pense no componente scalffold como a estruturação da sua tela. Ele calcula os espaços automaticamente. Por exemplo, se você colocar uma TopBar, o Scaffold empurra o seu texto um pouco para baixo.

![250](../../../attachments/Pasted%20image%2020260318084224.png)
![550](../../../attachments/Pasted%20image%2020260318084306.png)
![450](../../../attachments/Pasted%20image%2020260318084334.png)

Depois de criado a função composable, basta iserir no setContent.
![400](../../../attachments/Pasted%20image%2020260318084245.png)

---

**Scaffold na MainActivity**
- Elementos como a TopAppBar e BottomNavigation tornam-se persistentes. Ao navegar entre telas, essas barras permanecem estáticas, e apenas o conteúdo central (o corpo) é trocado.
- Como o Scaffold está fora do NavHost, as animações de transição de tela ocorrerão apenas no conteúdo interno. As barras não participarão da animação.
- É ideal para aplicativos que possuem uma estrutura de navegação global constante, onde a maioria das telas compartilha o mesmo menu inferior ou barra superior.

**Scaffold dentro de uma Tela específica/composable**
- Permite que cada tela tenha uma configuração única. 
- Ao navegar para uma nova tela, todo o layout (incluindo as barras) participa da animação de transição.
- Ideal para aplicativos onde as telas são visualmente muito distintas entre si ou quando você precisa de controle total sobre os componentes de interface de cada rota.
