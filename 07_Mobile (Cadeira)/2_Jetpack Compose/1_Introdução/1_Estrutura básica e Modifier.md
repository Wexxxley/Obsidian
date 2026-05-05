
#Concluded 

---
### **1. Estrutura inicial**

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

O **Scaffold** é um componente que implementa o layout visual básico do Material Design com espaços reservados para barras superiores, barras inferiores e botões flutuantes. 
- Quando o Scaffold é desenhado, ele calcula o espaço ocupado por elementos como a TopAppBar. Para evitar que o seu conteúdo principal fique escondido sob essas barras, o `Scaffold` passa um objeto do tipo `PaddingValues` através de uma expressão lambda.

---
### **2. Modifier**

O **Modifier** é uma interface que representa uma coleção ordenada de elementos de decoração. A recomendação oficial é que quase todo componente aceite um parâmetro modifier. Quem chama a sua função deve ter o poder de decidir onde ela ficará posicionada ou qual o seu tamanho externo.

>[!tip]
>**A ordem em que você encadeia os modificadores altera o resultado final**. Cada chamada de função no Modifier encapsula o componente subjacente em uma nova camada de restrições 

Por exemplo, aplicar um padding e depois um background resultará em um fundo colorido que respeita a margem interna. Inverter a ordem, aplicando primeiro o `background` e depois o `padding`, fará com que a cor de fundo preencha todo o espaço externo e, em seguida, o conteúdo interno seja empurrado para o centro. 

**Modificadores de Dimensão**
- **`fillMaxSize()`, `fillMaxWidth()`, `fillMaxHeight()`:** Instruem o componente a consumir todo o espaço remanescente disponibilizado pelo seu contêiner pai.
- **`size(width: Dp, height: Dp)`:** Força o componente a adotar dimensões absolutas.    
- **`weight(Float)`:** Aplicável a componentes contidos dentro de Row ou Column. 

**Modificadores de Espaçamento e Posicionamento**
- **`padding()`:** Aplica um recuo físico ao redor do limite atual do componente. 
- **`offset(x: Dp, y: Dp)`:** Desloca o componente visualmente em relação à sua posição matemática original.  A nova posição pode sobrepor outros elementos.

**Modificadores Visuais e de Desenho**
- **`background(color: Color, shape: Shape)`:** Pinta a área delimitada do componente com a cor especificada. O parâmetro `shape` permite que a pintura assuma contornos geométricos como `RoundedCornerShape` ou `CircleShape`.
- **`border(width: Dp, color: Color, shape: Shape)`:** Desenha borda.
- **`clip(shape: Shape)`:** Restringe a área de renderização visual do componente base e de todos os seus filhos a um formato geométrico pré-definido. 
- **`alpha(alpha: Float)`:** Opacidade`0.0f` (transparente) a `1.0f` (totalmente opaco).

**Modificadores de Interatividade e Eventos**
- **`clickable { onClick }`:** Habilita a detecção de eventos de toque (tap) na área delimitada.    
- **`verticalScroll()` e `horizontalScroll()`:** Injetam a capacidade de deslocamento de viewport em contêineres estáticos. Não são recomendados para coleções contendo um volume alto de dados.
- `selectable` Ele herda a capacidade de detecção de toque, mas impõe um contexto voltado para estados de escolha. Params: `selected: Boolean` e `onClick = {}`