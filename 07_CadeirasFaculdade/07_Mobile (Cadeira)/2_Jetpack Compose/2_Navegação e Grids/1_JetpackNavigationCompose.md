
#Concluded

---
![200](../../../../attachments/Pasted%20image%2020260501095550.png) ![200](../../../../attachments/navigation.gif)

**MainActivity**
![](../../../../attachments/Pasted%20image%2020260501100036.png)
**navController**: detentor de estado da navegação. Objeto que sabe em qual tela o usuário está. Gerencia uma pilha, cada vez que você navega, ele empilha um nó no objeto.

ScreenStructure utiliza o padrão de **State Hoisting** para gerenciar três sistemas complexos: o menu lateral, a barra de navegação e o conteúdo central.
![500](../../../../attachments/Pasted%20image%2020260501100544.png)
- **drawerState**: Controla se o menu lateral está aberto ou fechado. 
- **scope = rememberCoroutineScope()**: Operações como abrir ou fechar o menu são animações que levam tempo. Você precisa de um escopo de corrotina para dispará-las de dentro de cliques de botões comuns.
- **currentRoute**: Sempre que a tela muda, o currentBackStackEntryAsState avisa o Compose, permitindo que o menu ou a barra saibam qual item deve ser destacado.

**ModalNavigationDrawer**:
- **drawerContent**: Aqui você define o que está dentro do menu. 
- **onItemClick**:Quando você clica em um item do menu, três coisas acontecem:
    1. **navController.navigate**: O comando de mudança de tela é enviado.
    2. **popUpTo**: Remove vértices intermediários durante a transição.
    3. **launchSingleTop**: evita duplicatas de tela na árvore.
    4. **scope.launch { drawerState.close() }**: O menu não fecha sozinho por padrão. Você precisa instruí-lo a fechar animadamente.

![500](../../../../attachments/Pasted%20image%2020260501102243.png)
**NavHost**:
- Ele cria um grafo de telas. Ele fica "escutando" as mudanças no NavController. 
- É preciso registrar as telas.
- É preciso ter um nó inicial. Por padrão, o sistema de navegação do Android tenta manter esse nó na base da pilha.
**NavGraph**: Telas registradas.
- **Registro de Destinos:** Cada função composable("rota") registra um vértice.
