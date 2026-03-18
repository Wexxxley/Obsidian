

--- 
Existem basicamente 3 layouts em jetpack componentes: Column, row and box. Como o Compose não sabe onde colocar os elementos por padrão, você usa esses três "containers" para organizar o layout.

![](../../attachments/Pasted%20image%2020260318063308.png)
### **1. Column**

Ele recebe como parâmetros:
- **modifier**
- **verticalArrangement**: Controla o posicionamento no Eixo Principal.
- **horizontalAlignment**: Controla o posicionamento no **Eixo Cruzado** (Horizontal).
    
    - Ex: `Alignment.CenterHorizontally`, `Alignment.End`.
        

---

## 2. Row (Linha)

A **Row** organiza os elementos na **horizontal**.

## O que ela recebe (Parâmetros principais):

- **`horizontalArrangement`**: Controla o posicionamento no **Eixo Principal** (Horizontal).
    
    - Ex: `Arrangement.End` (empurra tudo para a direita), `Arrangement.spacedBy(8.dp)` (espaço fixo entre itens).
        
- **`verticalAlignment`**: Controla o posicionamento no **Eixo Cruzado** (Vertical).
    
    - Ex: `Alignment.CenterVertically` (alinha o texto e o ícone pelo meio).
        

---

## 3. Os conceitos de Arrangement vs. Alignment

Essa é a maior dúvida de quem está começando. A regra é simples:

1. **Arrangement (Arranjo):** Cuida do **Eixo Principal** (onde os itens "andam"). Na Column é a altura; na Row é a largura. Ele decide o **espaçamento** entre os filhos.
    
2. **Alignment (Alinhamento):** Cuida do **Eixo Cruzado**. Na Column é a largura; na Row é a altura. Ele decide onde o bloco inteiro se "encosta" (esquerda, direita, topo, baixo).
    

---

## 4. O parâmetro `Weight` (Peso)

Dentro de uma `Row` ou `Column`, você pode usar o `Modifier.weight()`. Isso é extremamente útil para o seu projeto de **Categorias**.

Imagine que você quer uma linha com o nome da categoria e o valor da despesa, mas quer que o nome ocupe todo o espaço e o valor fique no cantinho:

Kotlin

```
Row(modifier = Modifier.fillMaxWidth()) {
    Text("Alimentação", modifier = Modifier.weight(1f)) // Ocupa o que sobrar
    Text("R$ 50,00") // Ocupa apenas o seu próprio tamanho
}
```

---

## 5. Como funcionam "por baixo do pano"

Quando o Compose lê uma `Column`, ele faz o seguinte:

1. Mede o tamanho de cada filho (cada `Text`, `Button`, etc).
    
2. Soma as alturas (se for Column) ou larguras (se for Row).
    
3. Aplica o `Arrangement` para decidir onde colocar os espaços vazios.
    
4. Desenha tudo na tela de uma vez.
    

## Exemplo Prático de Uso Combinado:

No seu app, um item da lista de despesas seria uma mistura dos dois:

- Uma **Row** principal (para ícone e textos lado a lado).
    
- Uma **Column** dentro dessa Row (para o título da categoria e a data, um embaixo do outro).
    

Kotlin

```
Row {
    Icon(Icons.Default.Category, contentDescription = null)
    Column {
        Text("Mercado")
        Text("18/03/2026", fontSize = 12.sp)
    }
}
```

**Ficou clara a diferença de quando usar `Arrangement` e quando usar `Alignment`? Se quiser, posso te passar um desafio rápido de layout para você testar no seu código!**