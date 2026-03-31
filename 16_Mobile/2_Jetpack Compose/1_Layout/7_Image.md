
#Concluded 

---
Image no Compose é uma função que desenha um objeto do tipo `Painter`:
- **Painter:** É uma abstração para algo que pode ser desenhado. Pode ser um `BitmapPainter` (.jpg, .png) ou um `VectorPainter` (para ícones .xml). 
- **ContentDescription:** Serve para descrever imagens para users com deficiência visual.
- **Modifier:** Como em qualquer Composable.

**Imagens de Bitmap (PNG, JPEG, WEBP)**: Usamos a função `painterResource` .
```kotlin
Image(
    painter = painterResource(id = R.drawable.minha_foto),
    contentDescription = "Descrição da foto para acessibilidade",
    modifier = Modifier.size(200.dp)
)
```

**Ícones Vetoriais**: O Android Studio fornece uma biblioteca de ícones `Icons.Default`
```kotlin
Image(
    imageVector = Icons.Default.Favorite,
    contentDescription = "Ícone de coração",
    colorFilter = ColorFilter.tint(Color.Red)
)
```

O parâmetro **contentScale** determina como a imagem deve se comportar quando o tamanho do arquivo é diferente do tamanho do container (Modifier.size).
- **Crop:** Corta a imagem para preencher todo o espaço.
- **Fit:** Mantém a proporção mas pode deixar espaços vazios.
- **FillBounds:** Estica a imagem para preencher o espaço, ignorando a proporção.

![450](../../../attachments/Pasted%20image%2020260322081943.png)
![200](../../../attachments/Pasted%20image%2020260322081957.png)


