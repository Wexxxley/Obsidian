
#Concluded 

---
**Jetpack Compose** é um kit de ferramentas para construir UI Android nativa. O Jetpack Compose usa programação declarativa.

**Programação declarativa**: Esse padrão permite aos desenvolvedores projetar a interface do usuário com base nos dados recebidos. Este paradigma de design usa uma linguagem de programação para criar um aplicativo inteiro.

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            Text(text = "Hello World")
        }
    }
}
```

Um **Composable** é uma função marcada com a anotação `@Composable`. Ela é a unidade básica de UI. Em vez de retornar um objeto, ela "emite" componentes na tela.
```kotlin
@Composable
fun Saudacao(nome: String) {
    Text(text = "Olá, $nome!")
}
```

Esse é o codigo padrão quando você cria um novo projeto com jetpack component:
![570](../../attachments/Pasted%20image%2020260318071737.png)
 1. **MainActivity**: Activity é a tela que o usuário vê.
	- **`onCreate`**: É o primeiro método chamado quando o app abre.
	- **`enableEdgeToEdge()`**: Faz com que o conteúdo do app use toda a tela.
    - **`setContent { ... }`**: É aqui que você define o que está dentro do app
	- **`TestesTheme`**: É o Composable de estilo do seu projeto. Esse nome foi gerado automaticamente com base no nome do projeto. Tudo o que você coloca dentro dele vai herdar as cores, fontes e estilos que estão definidos nos arquivo theme do seu projeto.
	- **`Scaffold`**: O Scaffold é um componente com a estruturação da sua tela que já tem espaços reservados para: TopBar, BottomBar, Content.

2. **O Componente Greeting**: Função criada para mostrar algo na tela:
	- **`modifier`**: No código de cima, ele recebe o `innerPadding` do Scaffold para garantir que o texto tenha o espaçamento correto.
	
    - **`Text`**: A função pronta do Android que desenha o texto na tela.

3. **GreetingPreview**: `@Preview` Renderiza o design ao lafo do codigo
