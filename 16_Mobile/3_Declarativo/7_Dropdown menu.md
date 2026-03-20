

---

O componente permite que o usuário selecione um item de uma lista suspensa para realizar ações ou preencher campos. O menu não é um componente único, mas uma combinação de elementos que trabalham juntos:

- **Box:** Utilizado como contêiner principal.
- **Row/Text/Image:** Servem como o "gatilho" visual que o usuário clica para abrir a lista.
- **DropDownMenu:** O componente que contém a lista suspensa.
- **DropdownMenuItem:** Cada opção individual dentro do menu.

## 2. Parâmetros Fundamentais do DropDownMenu

O componente depende de dois estados principais para funcionar:

- **expanded (Boolean):** Controla a visibilidade do menu. Se `true`, o menu abre; se `false`, ele fecha.
    
- **onDismissRequest:** Um _callback_ acionado quando o usuário clica fora do menu ou pressiona o botão voltar. Geralmente, define-se o estado `expanded` como `false` aqui.
    

## 3. Gerenciamento de Estado e Dinamismo

Para evitar código repetitivo e complexo, o instrutor utiliza uma abordagem baseada em listas e índices:

- **Lista de Itens:** Uma `listOf` contendo as strings (ex: nomes de países).
    
- **Estado da Posição:** Uma variável `itemPosition` (Int) criada com `remember { mutableStateOf(0) }` para armazenar o índice do item selecionado.
    
- **Loop forEach:** O menu percorre a lista de países e cria um `DropdownMenuItem` para cada um automaticamente.
    

## 4. Integração com o arquivo `strings.xml`

Uma prática de organização recomendada na aula é mover a lista de dados para os recursos do Android:

- **string-array:** Criado no arquivo `res/values/strings.xml`. Isso separa os dados da lógica do código.
    
- **stringArrayResource:** Função utilizada no Kotlin para recuperar essa lista: `stringArrayResource(R.array.country_list)`.
    

## 5. Exemplo de Código Unificado

Abaixo, apresento a implementação simplificada baseada na explicação da aula:

Kotlin

```
@Composable
fun DropDownExemplo() {
    // 1. Dados e Estados
    val paises = listOf("Alemanha", "Inglaterra", "Itália", "Brasil")
    var expandido by remember { mutableStateOf(false) }
    var indiceSelecionado by remember { mutableStateOf(0) }

    Column(
        modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        // 2. O "Box" é essencial para o menu aparecer no lugar certo
        Box {
            Row(
                modifier = Modifier
                    .clickable { expandido = true } // Abre o menu ao clicar
                    .padding(16.dp),
                verticalAlignment = Alignment.CenterVertically
            ) {
                Text(text = paises[indiceSelecionado])
                Icon(Icons.Default.ArrowDropDown, contentDescription = null)
            }

            // 3. O Componente de Menu
            DropdownMenu(
                expanded = expandido,
                onDismissRequest = { expandido = false }
            ) {
                paises.forEachIndexed { indice, nome ->
                    DropdownMenuItem(
                        text = { Text(text = nome) },
                        onClick = {
                            indiceSelecionado = indice // Atualiza o índice
                            expandido = false // Fecha o menu
                        }
                    )
                }
            }
        }
    }
}
```

## 6. Observações Técnicas

- **Rolagem Automática:** Se a lista for muito longa (como demonstrado no vídeo com muitos países), o `DropdownMenu` cria automaticamente uma barra de rolagem interna.
    
- **Ícones Vetoriais:** A aula ensina a adicionar ícones através do _Vector Asset Studio_ (R.drawable), garantindo que a imagem não perca qualidade em diferentes tamanhos de tela.
    

Deseja que eu explique como customizar as cores e fontes de cada item dentro do menu suspenso?