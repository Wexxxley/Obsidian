

---

O botão mais simples exige dois itens: onClick e content.

```kotlin
Button(onClick = { println("Botão clicado!") }) {
    Text("Clique aqui")
}
```

Tudo o que você coloca dentro do conteudo do botão se comporta como se estivesse dentro de uma Row. Por isso, se você colocar um `Icon` e um `Text`, eles ficarão automaticamente um ao lado do outro.

![](../../attachments/Pasted%20image%2020260319102931.png)
- **`shape`**: Define o arredondamento.
- **`contentPadding`**: Ajusta o espaçamento interno.
- `border`: Define borda

![](../../attachments/Pasted%20image%2020260319105716.png)