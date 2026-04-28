

---

**Dialog**: É uma janela flutuante que é renderizada sobreposta ao conteúdo principal do aplicativo.

- **Renderização Condicional:** a instanciação é controlada por uma instrução if. Quando a variável de estado se torna verdadeira, o bloco de código é alcançado e o Dialog é adicionado à árvore de renderização.
- **onDismissRequest:** É um parâmetro obrigatório que atua como um callback. O sistema operacional o invoca quando detecta que o usuário deseja fechar o diálogo (geralmente tocando fora da área visível.
- **DialogProperties:** Uma classe que permite configurar o comportamento da janela do diálogo junto ao sistema operacional.
- **Surface**: Dialog nativo não possui cor de fundo, bordas arredondadas ou sombra. O componente Surface é utilizado para materializar a interface gráfica. Ele aplica a cor de fundo padrão.

**ProgressIndicator**: Existem fundamentalmente dois tipos de indicadores de progresso nativos: o formato circular e o formato linear. Cada um deles pode operar em dois modos distintos: determinado e indeterminado.

```kotlin
@Composable
fun TelaMultiplosIndicadores() {
    var exibindoDialog by remember { mutableStateOf(false) }
    var progressoAtual by remember { mutableStateOf(0.0f) }
    val escopoCorrotina = rememberCoroutineScope()

    Column(
        modifier = Modifier.fillMaxSize(),
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Button(
            onClick = {
                exibindoDialog = true
                progressoAtual = 0.0f
            
                // Corrotina para simular o avanço do progresso
                escopoCorrotina.launch {
                    while (progressoAtual < 1.0f) {
                        delay(100) 
                        progressoAtual += 0.05f
                    }
                    delay(500) // Aguarda meio segundo ao concluir
                    exibindoDialog = false // Fecha o diálogo
                }
            }
        ) {
            Text("Mostrar Todos os Indicadores")
        }
    }

    if (exibindoDialog) {
        Dialog(
            onDismissRequest = { exibindoDialog = false },
            properties = DialogProperties(dismissOnBackPress = false, dismissOnClickOutside = false)
        ) {
            Surface(
                shape = MaterialTheme.shapes.medium,
                color = MaterialTheme.colorScheme.surface,
                tonalElevation = 8.dp
            ) {
                Column(
                    modifier = Modifier
                        .padding(24.dp)
                        .fillMaxWidth(),
                    horizontalAlignment = Alignment.CenterHorizontally,
                    verticalArrangement = Arrangement.spacedBy(24.dp) // Espaçamento entre os itens
                ) {
                    Text("Processamento em andamento...")

                    // 1. Circular Indeterminado
                    Column(horizontalAlignment = Alignment.CenterHorizontally) {
                        CircularProgressIndicator()
                        Text("Circular Indeterminado", style = MaterialTheme.typography.bodySmall)
                    }

                    // 2. Circular Determinado
                    Column(horizontalAlignment = Alignment.CenterHorizontally) {
                        CircularProgressIndicator(progress = { progressoAtual })
                        Text("Circular Determinado", style = MaterialTheme.typography.bodySmall)
                    }

                    // 3. Linear Indeterminado
                    Column(horizontalAlignment = Alignment.CenterHorizontally) {
                        LinearProgressIndicator(modifier = Modifier.fillMaxWidth())
                        Text("Linear Indeterminado", style = MaterialTheme.typography.bodySmall)
                    }

                    // 4. Linear Determinado
                    Column(horizontalAlignment = Alignment.CenterHorizontally) {
                        LinearProgressIndicator(
                            progress = { progressoAtual },
                            modifier = Modifier.fillMaxWidth()
                        )
                        Text("Linear Determinado", style = MaterialTheme.typography.bodySmall)
                    }
                }
            }
        }
    }
}
```

### Tipos de Indicadores de Progresso

- **CircularProgressIndicator:** Renderiza uma trilha circular. É frequentemente utilizado de forma centralizada na tela para bloquear a interface durante um carregamento global, ou em tamanhos reduzidos ao lado de botões de ação e ícones de sincronização.
    
- **LinearProgressIndicator:** Renderiza uma barra horizontal. Ocupa menos espaço vertical e é convencionalmente posicionado nas extremidades de contêineres, como no topo de páginas da web ou diretamente abaixo da barra superior de navegação (TopAppBar) do aplicativo.
    

### Modos de Operação (Indeterminado e Determinado)

A distinção entre as variações no código acima reside na presença ou ausência do parâmetro `progress`.

- **Modo Indeterminado:** Invocado quando o componente não recebe o parâmetro de progresso. O framework aplica uma animação contínua e cíclica. Este modo deve ser empregado exclusivamente quando a arquitetura do sistema não permite calcular a duração total da operação (por exemplo, aguardar o processamento inicial de um servidor remoto).
    
- **Modo Determinado:** Invocado quando a propriedade `progress` recebe uma função lambda ou um valor estático do tipo `Float`. O valor fornecido deve estar estritamente no intervalo entre `0.0f` (0%) e `1.0f` (100%). A renderização visual (o preenchimento do círculo ou da barra) será matematicamente proporcional ao valor fornecido. Este modo requer que o processo subjacente seja quantificável (por exemplo, o número de bytes baixados em relação ao total do arquivo).
    

### Gestão de Estado no Exemplo

No código apresentado, a transição do estado determinado é gerenciada através da variável `progressoAtual`. Uma estrutura de repetição (`while`) dentro de uma corrotina incrementa este valor a cada 100 milissegundos. O Jetpack Compose, ao detectar esta mutação de estado, aciona o mecanismo de recomposição, redesenhando a porção preenchida dos indicadores designados como "Determinados" na interface do usuário em tempo real.
