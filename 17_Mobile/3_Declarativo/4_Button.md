

---

O botão mais simples exige dois itens: onClick e content.

```kotlin
Button(onClick = { println("Botão clicado!") }) {
    Text("Clique aqui")
}
```

Tudo o que você coloca dentro do conteudo do botão se comporta como se estivesse dentro de uma Row. Por isso, se você colocar um `Icon` e um `Text`, eles ficarão automaticamente um ao lado do outro.

```kotlin
Button(
    onClick = { /* ação */ },
    enabled = true,
    shape = CircleShape, // Deixa o botão redondo
    colors = ButtonDefaults.buttonColors(
        containerColor = Color.Blue,
        contentColor = Color.White
    )
) {
    Icon(Icons.Default.Favorite, contentDescription = null)
    Spacer(Modifier.width(8.dp)) // Espaço entre ícone e texto
    Text("Favorito")
}
```
- **`enabled`**: Se `false`, o botão fica cinza e não clica.  
- **`shape`**: Define o arredondamento (ex: `RoundedCornerShape(8.dp)`).
- **`contentPadding`**: Ajusta o espaçamento interno.
