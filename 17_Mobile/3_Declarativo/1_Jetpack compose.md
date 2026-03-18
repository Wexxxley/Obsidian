

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
    - **`setContent { ... }`**: Você define a interface diretamente com funções Kotlin dentro deste bloco.
	- **`TestesTheme`**: É o Composable de estilo do seu projeto. Ele define as cores (Dark/Light mode), fontes e formas que o app vai usar.
    
- **`Scaffold`**: Pense nele como a **"Estrutura da Casa"**. O Scaffold facilita colocar elementos padrões do Android, como uma barra superior (TopBar), um botão flutuante ou um menu inferior.
    
    - **`innerPadding`**: O Scaffold calcula automaticamente o espaço das barras do sistema (como a de status) para que seu texto não fique "escondido" atrás delas.
        

---

## 3. O Componente `Greeting` (O Composable)

Esta é a função que você criou para mostrar algo na tela:

Kotlin

```
@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Text(
        text = "Hello $name!",
        modifier = modifier
    )
}
```

- **`name`**: Um parâmetro simples (uma String).
    
- **`modifier`**: É o "estilista" do componente. No código lá de cima, ele recebe o `innerPadding` do Scaffold para garantir que o texto tenha o espaçamento correto.
    
- **`Text`**: A função pronta do Android que desenha o texto na tela.
    

---

## 4. O Preview (`GreetingPreview`)

Esta parte não vai para o celular do usuário. Ela serve apenas para o **Android Studio**.

- **`@Preview`**: Diz ao IDE: "Ei, renderize isso aqui na aba 'Design' ao lado do código".
    
- **`showBackground = true`**: Coloca um fundo branco atrás do texto para você enxergar melhor como ele fica.
    

---

## Resumo do Fluxo:

1. O Android inicia a **Activity**.
    
2. O **`setContent`** ativa o motor do Compose.
    
3. O **`Scaffold`** prepara o terreno (espaçamentos).
    
4. A função **`Greeting`** é chamada, passando o nome "Android".
    
5. O **`Text`** finalmente "pinta" o texto na tela.
    

**Como você está estudando para o projeto de Categorias, quer que eu te mostre como transformar esse `Greeting` em uma lista simples usando `Column` e vários `Text`?**