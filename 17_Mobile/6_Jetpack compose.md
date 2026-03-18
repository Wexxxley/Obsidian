

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

A unidade básica do Compose é a função **@Composable.** Elas são funções Kotlin comuns, mas com uma anotação que diz ao compilador: "esta função transforma dados em elementos de UI".
![](../attachments/Pasted%20image%2020260318054955.png)



