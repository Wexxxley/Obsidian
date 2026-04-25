
---
![](../../../attachments/Pasted%20image%2020260425154906.png)

GridCells determina como o espaço cruzado (a largura na grade vertical ou a altura na grade horizontal) será dividido.
- **`GridCells.Fixed(count: Int)`:** Força a grade a ter um número exato e estático de colunas ou linhas, dividindo o espaço total disponível igualmente entre elas.
- **`GridCells.Adaptive(minSize: Dp)`:** Define um tamanho mínimo para cada célula. O Compose calculará automaticamente quantas colunas ou linhas cabem na tela do dispositivo atual respeitando esse tamanho mínimo. 

```kotlin
@Composable
fun ExemploGradeVertical() {
    LazyVerticalGrid(
        columns = GridCells.Fixed(3),

        contentPadding = PaddingValues(16.dp),
        
        // Adiciona espaçamento horizontal entre as colunas
        horizontalArrangement = Arrangement.spacedBy(8.dp),
        
        // Adiciona espaçamento vertical entre as linhas
        verticalArrangement = Arrangement.spacedBy(8.dp),
        
        modifier = Modifier.fillMaxSize()
    ) {
        items(50) { index ->
            CaixaItem(texto = "Item $index")
        }
    }
}
```

```kotlin
@Composable
fun ExemploGradeHorizontal() {
    LazyHorizontalGrid(
        // Define que cada linhaterá no mínimo 80.dp de altura.
        rows = GridCells.Adaptive(minSize = 80.dp),
        
        contentPadding = PaddingValues(16.dp),
        horizontalArrangement = Arrangement.spacedBy(8.dp),
        verticalArrangement = Arrangement.spacedBy(8.dp),
        
        modifier = Modifier.height(300.dp).fillMaxWidth()
    ) {
        items(50) { index ->
            CaixaItem(texto = "H-Item $index")
        }
    }
}
```
