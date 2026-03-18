

---
Jetpack Compose é um kit de ferramentas para construir UI Android nativa. O Jetpack Compose usa programação declarativa.

**Imperativa**: Este paradigma envolve ter um modelo separado da UI do aplicativo.
```xml
<TextView
    android:id="@+id/tv_name"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
/>
```

```java
public class MainActivity extends AppCompatActivity {

    TextView tvName;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_checkbox);
        tvName = findViewById(R.id.tv_name);
        tvName.setText("Hello World");
    }
}
```

**Declarativa**: Esse padrão permite aos desenvolvedores projetar a interface do usuário com base nos dados recebidos. Este paradigma de design usa uma linguagem de programação para criar um aplicativo inteiro.

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


![](../../attachments/Pasted%20image%2020260318071737.png)
Esse é o codigo padrão quando você cria um novo projeto com jetpack component
 
 1. **MainActivity**: Activity é a tela que o usuário vê.
	- **`onCreate`**: É o primeiro método chamado quando o app abre.
	
	- **`enableEdgeToEdge()`**: Faz com que o conteúdo do app use toda a tela.
	
    - **`setContent { ... }`**: É aqui que você define o que está dentro do app
    
	- **`TestesTheme`**: É o Composable de estilo do seu projeto. Esse nome foi gerado automaticamente com base no nome do projeto. Tudo o que você coloca dentro dele vai herdar as cores, fontes e estilos que estão definidos nos arquivo theme do seu projeto.

	- **`Scaffold`**: O nome Scaffold significa "Andaime". No Android, o Scaffold é um componente que já vem com os "buracos" prontos para as partes comuns de um app.

Pense no `Scaffold` como uma tela que já tem espaços reservados para:

- **TopBar:** Barra de título no topo.
    
- **BottomBar:** Menu de navegação embaixo.
    
- **FloatingActionButton:** Aquele botão redondo de "+" que fica flutuando.
    
- **Content:** O conteúdo principal (onde fica o seu texto ou lista).
    

**Por que usamos ele?** Porque ele calcula os espaços automaticamente. Por exemplo, se você colocar uma `TopBar`, o `Scaffold` empurra o seu texto um pouco para baixo para que eles não fiquem um em cima do outro.


2. O Componente Greeting: Função criada para mostrar algo na tela:
	- **`modifier`**: No código de cima, ele recebe o `innerPadding` do Scaffold para garantir que o texto tenha o espaçamento correto.
	
    - **`Text`**: A função pronta do Android que desenha o texto na tela.

3. **GreetingPreview**: `@Preview` Renderiza o design ao lafo do codigo

## 2. O que é o Scaffold? (A "Armação")

O nome **Scaffold** significa **"Andaime"**. Em engenharia, um andaime serve para segurar a estrutura enquanto você constrói. No Android, o `Scaffold` é um componente que já vem com os "buracos" prontos para as partes comuns de um app.

Pense no `Scaffold` como uma tela que já tem espaços reservados para:

- **TopBar:** Barra de título no topo.
    
- **BottomBar:** Menu de navegação embaixo.
    
- **FloatingActionButton:** Aquele botão redondo de "+" que fica flutuando.
    
- **Content:** O conteúdo principal (onde fica o seu texto ou lista).
    

**Por que usamos ele?** Porque ele calcula os espaços automaticamente. Por exemplo, se você colocar uma `TopBar`, o `Scaffold` empurra o seu texto um pouco para baixo para que eles não fiquem um em cima do outro.

---

## 3. Por que o Tema recebe o Scaffold?

No Kotlin/Compose, quando uma função "recebe" outra (o que fica entre as chaves `{ }`), significa que a de fora está **aplicando regras** na de dentro.

Kotlin

```
TestesTheme {        // 1. Aplica as CORES e FONTES do seu projeto
    Scaffold {       // 2. Prepara a ESTRUTURA da tela (topo, fundo, etc)
        Greeting()   // 3. Desenha o CONTEÚDO real
    }
}
```

**A lógica é a seguinte:**

1. O **Tema** precisa envolver tudo para que o `Scaffold` e o `Greeting` saibam quais cores usar (se o fundo é branco ou preto, por exemplo).
    
2. O **Scaffold** envolve o seu conteúdo (`Greeting`) para garantir que ele fique posicionado corretamente, respeitando as margens do sistema.
    

## Um exemplo para o seu projeto de Categorias:

Se você quiser colocar um título no topo do seu app, o `Scaffold` facilita muito:

Kotlin

```
Scaffold(
    topBar = {
        Text("Minhas Categorias", modifier = Modifier.padding(16.dp))
    }
) { innerPadding ->
    // O conteúdo principal vai aqui e usa o 'innerPadding' para não bater na TopBar
    Column(modifier = Modifier.padding(innerPadding)) {
        Text("Alimentação")
        Text("Transporte")
    }
}
```

---

## Resumo:

- **`TestesTheme`**: É o balde de tinta (define as cores do seu projeto "testes").
    
- **`Scaffold`**: É o esqueleto da tela (organiza onde fica o topo e o rodapé).
    
- **A hierarquia**: O Tema manda no visual do Scaffold, e o Scaffold manda na posição do seu conteúdo.
    

**Ficou mais claro agora por que um fica dentro do outro? Se quiser, posso te mostrar onde ficam os arquivos do `TestesTheme` para você mudar a cor do seu app.**