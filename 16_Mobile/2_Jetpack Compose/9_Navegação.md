


---

Antes de codificar, é preciso entender três pilares do Navigation Compose:

- **NavController:** É o motor central. Ele mantém o estado da "pilha de telas" (back stack) e permite realizar a navegação entre elas.
    
- **NavHost:** É um container visual que exibe o conteúdo da rota atual. Ele associa o `NavController` a um gráfico de navegação.
    
- **NavGraph (Gráfico de Navegação):** Define quais são as telas (destinos) disponíveis no app e como elas se conectam via rotas (strings que funcionam como URLs).
    

No exemplo da aula, o instrutor preparou o ambiente criando arquivos separados para manter o código limpo (_Clean Code_).

## 1.1 Preparação da MainActivity

A `MainActivity` deixa de conter a lógica da interface e passa a chamar apenas a função principal que gerenciará o fluxo.

Kotlin

```
// No MainActivity.kt
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            NavigationExampleTheme {
                // Aqui chamaremos o componente de navegação que veremos adiante
                MainPage() 
            }
        }
    }
}
```

---

## Parte 2: Construção da UI da Main Page (Primeira Tela)

Nesta etapa, o foco é criar os componentes de entrada de dados e aplicar o estado (_State_) para capturar o que o usuário digita.

## 2.1 Gerenciamento de Estado

Para que o Compose "lembre" o que foi digitado, usamos o `remember` e `mutableStateOf`.

- **`mutableStateOf("")`**: Cria um estado que, ao ser alterado, dispara uma recomposição (atualização da tela).
    
- **`remember`**: Garante que o valor não seja resetado toda vez que a função for executada novamente.
    

Kotlin

```
val username = remember { mutableStateOf("") }
val userAge = remember { mutableStateOf("") }
```

## 2.2 Estrutura com Scaffold e TopAppBar

O `Scaffold` é um layout padrão do Material Design que facilita a inserção de barras superiores, barras inferiores e botões flutuantes.

Kotlin

```
@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun MainPage() {
    Scaffold(
        topBar = {
            TopAppBar(
                title = { Text(text = "Main Page", color = Color.White, fontSize = 20.sp) },
                colors = TopAppBarDefaults.smallTopAppBarColors(
                    containerColor = Color(0xFF6200EE) // Purple 500
                )
            )
        },
        content = { paddingValues ->
            Column(
                modifier = Modifier
                    .fillMaxSize()
                    .padding(paddingValues),
                verticalArrangement = Arrangement.Center,
                horizontalAlignment = Alignment.CenterHorizontally
            ) {
                // Campos de Texto e Botão aqui
            }
        }
    )
}
```

## 2.3 Componentes de Entrada (TextField e Button)

Detalhes importantes explicados na aula:

- **`onValueChange`**: Atualiza a variável de estado com o novo caractere digitado (`it`).
    
- **`keyboardOptions`**: No campo de idade, foi usado `KeyboardType.Number` para forçar o teclado numérico, melhorando a UX (User Experience).
    
- **Estilização**: Uso de `RoundedCornerShape` para bordas arredondadas e `TextFieldDefaults` para remover a linha inferior padrão (indicador transparente).
    

---

## Parte 3: Construção da Second Page (Segunda Tela)

A segunda tela é mais simples, focada em exibir os dados que serão recebidos.

## 3.1 Ícone de Navegação (Botão Voltar)

Diferente da primeira tela, a `TopAppBar` da segunda tela inclui o `navigationIcon`.

Kotlin

```
navigationIcon = {
    IconButton(onClick = { /* Lógica de voltar virá depois */ }) {
        Icon(
            imageVector = Icons.Filled.ArrowBack,
            contentDescription = "Back",
            tint = Color.White
        )
    }
}
```

Nesta tela, foram usados apenas componentes `Text` e `Spacer` para organizar a exibição do Nome e da Idade que foram enviados.

---

## Resumo Técnico dos Termos Usados:

- **Composable Function:** Funções marcadas com `@Composable` que definem a interface.
    
- **Modifier:** Ferramenta para alterar o comportamento ou aparência de um componente (tamanho, padding, cliques).
    
- **Arrangement vs Alignment:** No `Column`, _Arrangement_ cuida do espaçamento vertical e _Alignment_ do alinhamento horizontal.
    
- **sp vs dp:** `sp` (Scale-independent Pixels) é usado para fontes, respeitando as configurações de acessibilidade do usuário. `dp` (Density-independent Pixels) é usado para dimensões de layout.
    

**Deseja que eu prossiga para a explicação da lógica de implementação do NavHost e a passagem de parâmetros propriamente dita?**