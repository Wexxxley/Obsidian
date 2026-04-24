
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

**GreetingPreview**: Renderiza o design ao lado do codigo.

Versão com Scaffold e modifier
![570](../../../attachments/Pasted%20image%2020260318071737.png)

O **Scaffold** é um componente que implementa o layout visual básico do Material Design com espaços reservados para barras superiores, barras inferiores e botões flutuantes. 

O **Modifier** é uma interface que representa uma coleção ordenada de elementos de decoração.  A ordem das decorações importa; por exemplo, aplicar um `padding` antes de um `clickable` resultará em uma área de clique diferente.
- A recomendação oficial é que quase todo componente aceite um parâmetro modifier. Quem chama a sua função Composable deve ter o poder de decidir onde ela ficará posicionada ou qual o seu tamanho externo.
    
- **Encapsulamento:** Ao passar o modifier como parâmetro, você permite que o componente se integre corretamente ao layout do componente pai, mantendo a lógica interna isolada.
    

- **O papel do innerPadding:** Quando o `Scaffold` é desenhado, ele calcula o espaço ocupado por elementos como a `TopAppBar` ou a `NavigationBar`. Para evitar que o seu conteúdo principal fique escondido sob essas barras, o `Scaffold` passa um objeto do tipo `PaddingValues` (nomeado no seu código como `innerPadding`) através de uma expressão lambda.
    
- **Por que não passar o modifier completo?:** No seu código, dentro da lambda do `Scaffold`, você está instanciando o componente `Testando`. O parâmetro `modifier` do `Testando` recebe o resultado de `Modifier.padding(innerPadding)`.
    
- **Fluxo de dados:** 1. O `Scaffold` calcula as margens de segurança.
    
    2. Ele fornece esses valores via `innerPadding`.
    
    3. Você cria um modificador que aplica exatamente esse distanciamento.
    
    4. O componente `Testando` recebe esse modificador e o utiliza internamente para se posicionar corretamente, respeitando os limites das barras de interface.
    



### A sintaxe `modifier: Modifier = Modifier`

Essa expressão no cabeçalho da função é uma atribuição de parâmetro padrão do Kotlin, similar aos _Optional Parameters_ do C#.

- **`modifier: Modifier`**: Declara que a função espera um parâmetro chamado `modifier` que é do tipo da interface `Modifier`.
    
- **`= Modifier`**: Este é o valor padrão. O `Modifier` (com "M" maiúsculo e sem parênteses) refere-se ao objeto _companion_ singleton da interface, que representa um modificador vazio (sem nenhuma instrução de layout).
    
- **Utilidade:** Isso permite que você chame a função `Testando()` sem passar nenhum argumento, caso não queira aplicar nenhuma modificação externa.
    

- **modifier**: No código de cima, ele recebe o innerPadding do Scaffold para garantir que o texto tenha o espaçamento correto.
    - **Text**: A função pronta do Android que desenha o texto na tela.
