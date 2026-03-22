

---
Image no Compose é uma função que desenha um objeto do tipo `Painter` em um `Canvas`
- **Painter:** É uma abstração para algo que pode ser desenhado. Pode ser um `BitmapPainter` (para fotos como .jpg, .png) ou um `VectorPainter` (para ícones .xml). 
- **ContentDescription:** Serve para descrever imagens para users com deficiência visual.
- **Modifier:** Como em qualquer Composable.

Existem duas formas de carregar arquivos que estão dentro da sua pasta `res/drawable`:

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

---

## 3. Escalonamento e Recorte (ContentScale)

O parâmetro `contentScale` determina como a imagem deve se comportar quando o tamanho do arquivo é diferente do tamanho do container (`Modifier.size`).

- **ContentScale.Crop:** Corta a imagem para preencher todo o espaço (comum em fotos de perfil).
    
- **ContentScale.Fit:** Mantém a proporção e garante que a imagem inteira apareça (pode deixar espaços vazios).
    
- **ContentScale.FillBounds:** Estica a imagem para preencher o espaço, ignorando a proporção (causa distorção).
    

---

## 4. Exemplo Completo: Card de Usuário Personalizado

Este exemplo une carregamento de recurso, recorte circular, bordas e redimensionamento.

Kotlin

```
@Composable
fun UserProfileImage() {
    Column(
        modifier = Modifier.fillMaxWidth().padding(16.dp),
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Image(
            painter = painterResource(id = R.drawable.profile_placeholder),
            contentDescription = "Foto de perfil do usuário",
            modifier = Modifier
                .size(120.dp) // Define o tamanho
                .clip(CircleShape) // Corta a imagem em formato de círculo
                .border(2.dp, Color.Gray, CircleShape), // Adiciona uma borda
            contentScale = ContentScale.Crop // Garante que preencha o círculo
        )
        
        Spacer(modifier = Modifier.height(8.dp))
        
        Text(text = "Wesley Freitas", fontSize = 20.sp)
    }
}
```

---

## 5. Imagens da Internet (Biblioteca Coil)

O componente `Image` nativo **não** carrega URLs (ex: `https://...`) diretamente. Para isso, a indústria usa a biblioteca **Coil**, que é otimizada para o Compose.

**No `build.gradle.kts`:**

Kotlin

```
implementation("io.coil-kt:coil-compose:2.5.0")
```

**No Código:**

Kotlin

```
AsyncImage(
    model = "https://meusite.com/imagem.png",
    contentDescription = "Imagem carregada da rede",
    modifier = Modifier.fillMaxWidth(),
    placeholder = painterResource(R.drawable.loading), // Imagem enquanto carrega
    error = painterResource(R.drawable.error_icon)    // Imagem se falhar
)
```

---

## Resumo Técnico para CC:

- **Gestão de Recursos:** O sistema `R.drawable` gera IDs inteiros que apontam para recursos compilados.
    
- **Memória:** Imagens grandes podem causar `OutOfMemoryError`. Bibliotecas como Coil lidam com o _downsampling_ (reduzir a resolução da imagem para caber na tela) e _caching_ (armazenamento local para não baixar de novo).
    
- **Acessibilidade:** Nunca deixe o `contentDescription` vazio em elementos que transmitem informação. Use `null` apenas para imagens puramente decorativas.
    

**Gostaria que eu explicasse como criar formas customizadas (como um hexágono) para recortar sua imagem?**