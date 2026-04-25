
#Concluded 

---
Jetpack Compose é um kit de ferramentas para construir UI Android nativa. 

Um **Composable** é uma função marcada com `@Composable`. Em vez de retornar um objeto, ela "emite" componentes na tela.
```kotlin
@Composable
fun Saudacao(nome: String) {
    Text(text = "Olá, $nome!")
}
```

Esse é o codigo padrão quando você cria um novo projeto com jetpack component:
![400](../../../attachments/Pasted%20image%2020260424133858.png)
 **MainActivity**: Activity é a tela que o usuário vê.
- **onCreate**: É o primeiro método chamado quando o app abre.
- **enableEdgeToEdge()**: Faz com que o conteúdo do app use toda a tela.
- **setContent**: É aqui que você define o que está dentro do app
- **TestesTheme**: Composable de estilo do projeto. Nome gerado automaticamente.

**Componente**: Função criada para mostrar algo na tela:

**Preview**: Renderiza o design ao lado do codigo.

Versão com Scaffold e modifier
![570](../../../attachments/Pasted%20image%2020260318071737.png)

O **Modifier** é uma interface que representa uma coleção ordenada de elementos de decoração. A recomendação oficial é que quase todo componente aceite um parâmetro modifier. Quem chama a sua função deve ter o poder de decidir onde ela ficará posicionada ou qual o seu tamanho externo.

O **Scaffold** é um componente que implementa o layout visual básico do Material Design com espaços reservados para barras superiores, barras inferiores e botões flutuantes. 
- Quando o Scaffold é desenhado, ele calcula o espaço ocupado por elementos como a TopAppBar. Para evitar que o seu conteúdo principal fique escondido sob essas barras, o `Scaffold` passa um objeto do tipo `PaddingValues` através de uma expressão lambda.
