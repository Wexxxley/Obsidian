

---
### **1. CheckBox**

O componente Checkbox é para permitir que o usuário selecione uma ou mais opções de um conjunto, ou confirme um estado binário.  O Checkbox depende de uma variável booleana externa.
- **value:** Um parâmetro booleano.
- **onCheckedChange:** Uma função de retorno (callback) disparada sempre que o usuário interage com o componente. 

![](../../attachments/Pasted%20image%2020260319181215.png)
![](../../attachments/checkBoxSimples.gif)


Por padrão, o componente `Checkbox` do Material Design é apenas o quadrado de marcação. Ele não inclui um rótulo de texto automaticamente.
- **Uso de Row:** É necessário envolver o `Checkbox` e um `Text` dentro de uma `Row` para criar um item de formulário legível.
- **Área de Clique:** Para melhorar a usabilidade, recomenda-se aplicar o `Modifier.clickable` na Row inteira.

---
### **2. RadioButton**

O **RadioButton** é o componente utilizado no Material Design para permitir que o usuário selecione exatamente uma opção de um conjunto de escolhas mutuamente exclusivas. 

O grupo de RadioButtons geralmente é controlado por uma única variável que armazena a opção selecionada no momento. 

O componente possui as seguintes propriedades fundamentais em sua assinatura:
- **selected:** Define se o botão está preenchido. 
- **onClick**: O evento disparado ao clicar no botão. Diferente do Checkbox, ele não retorna um booleano, pois o clique em um RadioButton sempre significa a intenção de selecioná-lo.    



Para garantir uma boa experiência de uso, os RadioButtons devem ser organizados dentro de uma `Column` ou `Row`, acompanhados de rótulos de texto.

```
// 1. Definição das opções possíveis
val opcoesSet = listOf("Cartão de Crédito", "Boleto Bancário", "Pix")

// 2. Estado que armazena a opção atualmente escolhida (inicialmente a primeira)
var opcaoSelecionada by remember { mutableStateOf(opcoesSet[0]) }

Column(modifier = Modifier.padding(16.dp)) {
    Text(text = "Selecione a forma de pagamento:", fontSize = 18.sp)

    opcoesSet.forEach { textoOpcao ->
        Row(
            modifier = Modifier
                .fillMaxWidth()
                .height(56.dp)
                // Centralização da lógica de clique na linha inteira
                .selectable(
                    selected = (textoOpcao == opcaoSelecionada),
                    onClick = { opcaoSelecionada = textoOpcao }
                )
                .padding(horizontal = 16.dp),
            verticalAlignment = Alignment.CenterVertically
        ) {
            RadioButton(
                selected = (textoOpcao == opcaoSelecionada),
                // Definimos como null para que o clique seja gerenciado pela Row (selectable)
                onClick = null 
            )
            Text(
                text = textoOpcao,
                modifier = Modifier.padding(start = 16.dp),
                fontSize = 16.sp
            )
        }
    }
}
```

## 4. O Modificador .selectable

No exemplo acima, utilizamos `Modifier.selectable` em vez de `.clickable`.

- **Propósito Técnico:** O `selectable` é otimizado para componentes de seleção única. Ele lida internamente com a acessibilidade, informando ao sistema que aquele item faz parte de um grupo onde apenas um pode estar ativo.
    
- **Lógica de Comparação:** A propriedade `selected` recebe o resultado da expressão booleana `(textoOpcao == opcaoSelecionada)`. O Compose avalia isso para cada item da lista; apenas aquele que coincidir com o valor armazenado no estado será desenhado como selecionado.
    

## 5. Diferenças Cruciais entre Checkbox e RadioButton

- **Intencionalidade:** O Checkbox é para múltiplas escolhas independentes. O RadioButton é para uma escolha única obrigatória entre várias.
    
- **Comportamento de Clique:** Um Checkbox pode ser desmarcado clicando nele novamente (toggle). Um RadioButton, por padrão, não é desmarcado ao ser clicado novamente; ele permanece selecionado até que outra opção do grupo seja escolhida.
    

## 6. Agrupamento com Data Classes

Em sistemas complexos, em vez de usar uma lista de Strings, recomenda-se o uso de uma `data class` ou um `Enum` para representar as opções, garantindo que a comparação lógica seja feita através de IDs ou tipos específicos, evitando erros de digitação.

Deseja que eu demonstre como integrar este grupo de RadioButtons ao formulário de cadastro que desenvolvemos anteriormente?


