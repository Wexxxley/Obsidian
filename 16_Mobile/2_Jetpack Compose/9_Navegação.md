


---

É recomendado criar arquivos Kotlin separados para cada tela.
- **MainActivity.kt**: Fica apenas como o ponto de entrada.
- **MainPage.kt**: Conterá a interface da primeira tela.
- **SecondPage.kt**: Conterá a interface da segunda tela.

Antes de desenhar os componentes, o instrutor altera a cor da barra de status (onde fica o relógio e bateria) para combinar com o app. Isso é feito no arquivo `Theme.kt`.

Kotlin

```
// Dentro do arquivo Theme.kt
val myStatusBarColor = colorResource(id = R.color.purple_700)
val view = LocalView.current
if (!view.isInEditMode) {
    SideEffect {
        val window = (view.context as Activity).window
        // Converte a cor para o formato ARGB que o Android entende
        window.statusBarColor = myStatusBarColor.toARGB()
    }
}
```


## 4. Criando a TopAppBar na MainPage

O instrutor define uma barra superior com fundo roxo e título branco.

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
                    containerColor = colorResource(id = R.color.purple_500)
                )
            )
        },
        content = { paddingValues ->
            // O conteúdo da página entra aqui, usando o paddingValues
        }
    )
}
```

---

**Destaques desta parte:**

- **`colorResource`**: Busca cores definidas no arquivo XML de recursos antigo (`colors.xml`), facilitando a transição.
    
- **`sp` vs `dp`**: Lembre-se, `sp` é para textos (escala baseada na preferência do usuário) e `dp` para tamanhos de componentes.
    
- **`toARGB()`**: Um método necessário porque a API de Janelas do Android é antiga e não entende o objeto `Color` do Compose diretamente.
    

Quando estiver pronto para ver como ele constrói o formulário da primeira página e gerencia os estados dos campos de texto, diga **next**.