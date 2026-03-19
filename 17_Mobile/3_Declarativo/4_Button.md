

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

Usando estado no botão
![560](../../attachments/Pasted%20image%2020260319105716.png)
1. **remember:** O Compose redesenha a tela constantemente. O remember serve para o botão não "esquecer" o valor da variável toda vez que a função for executada.
2. **mutableStateOf:** É um tipo de variável especial. O Compose fica "vigiando" essa variável; se o valor dela muda, o Compose entende que teve mudanças.
3. **onClick:** Dentro do clique do botão, você altera o valor dessa variável. Essa mudança avisa o sistema: "Ei, o estado mudou, redesenhe a tela agora!".
