


---

É recomendado criar arquivos Kotlin separados para cada tela.
![](../../attachments/Pasted%20image%2020260321090519.png)

**MainPage**
![500](../../attachments/Pasted%20image%2020260321090626.png)
![520](../../attachments/Pasted%20image%2020260321090646.png)
![200](../../attachments/tela1.gif)

Para que a navegação aconteça, você precisa de uma **Estrutura de Controle** que gerencie as telas. 

O Jetpack Navigation é um Grafo Direcionado:


Até agora, você tem o código de um Nodo (`MainPage`), mas não declarou o Grafo no sistema Android.

Você precisa de um lugar central (geralmente na sua `MainActivity` ou em uma função separada) para definir esse grafo. Para isso, usamos três componentes do Google:

- **`navController`**: Ele sabe em qual tela o usuário está e guarda o histórico (pilha).
    
- **`NavHost`**: É o container visual. Ele decide qual Composable desenhar na tela baseada na rota ativa.
    
- **`composable("rota")`**: É onde você registra suas telas.

Para consertar seu projeto agora, você deve criar uma função (pode ser no mesmo arquivo da `MainPage` ou na `MainActivity`) que organize isso:

Kotlin

```
@Composable
fun AppNavigation() {
    // 1. Criamos o motor de navegação
    val navController = rememberNavController()

    // 2. Definimos o Host (o palco) e a tela inicial
    NavHost(navController = navController, startDestination = "tela_principal") {
        
        // 3. Registramos a sua MainPage
        composable("tela_principal") {
            // Importante: sua MainPage agora PRECISA receber o navController
            MainPage(navController) 
        }

        // 4. Registramos a SecondPage (que você criará a seguir)
        composable("segunda_tela") {
            SecondPage(navController)
        }
    }
}
```

---

## Por que sua `MainPage` precisa mudar?

Atualmente, o seu botão `Send` está vazio. Para ele funcionar, a função `MainPage` precisa "segurar" o `navController` para poder dar a ordem de navegação.

**Como deve ficar a assinatura da sua função:**

Kotlin

```
@Composable
fun MainPage(navController: NavController) { // <-- O controlador entra aqui
    // ... seu código de estados e Scaffold ...

    Button(
        onClick = { 
            // Agora o botão tem um destino!
            navController.navigate("segunda_tela") 
        }
    ) {
        Text("Send")
    }
}
```

