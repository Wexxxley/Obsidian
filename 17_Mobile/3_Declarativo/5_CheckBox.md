

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


**Exemplo completo**
```
// Estado que controla se o componente está marcado ou não
var notifyByEmail by remember { mutableStateOf(false) }

Row(
    modifier = Modifier
        .fillMaxWidth()
        .padding(16.dp)
        .clickable { notifyByEmail = !notifyByEmail }, // Melhora a área de toque
    verticalAlignment = Alignment.CenterVertically
) {
    Checkbox(
        checked = notifyByEmail,
        onCheckedChange = { novoValor -> notifyByEmail = novoValor },
        enabled = true,
        colors = CheckboxDefaults.colors(
            checkedColor = Color.Blue,
            uncheckedColor = Color.Gray,
            checkmarkColor = Color.White,
            disabledCheckedColor = Color.LightGray
        ),
        interactionSource = remember { MutableInteractionSource() }
    )
    Text(
        text = "Receber notificações por e-mail",
        modifier = Modifier.padding(start = 8.dp)
    )
}
```

## Explicação das Propriedades

- **checked (Boolean):** Esta é a propriedade fundamental que define o estado visual do componente. Como o `Checkbox` é um componente "stateless" (sem estado interno próprio), ele apenas reflete o valor booleano que você passa para este parâmetro. Se o valor for `true`, o ícone de marcação aparece; se for `false`, o quadrado fica vazio.
    
- **onCheckedChange ((Boolean) -> Unit)?**: É o evento de retorno de chamada (callback). Ele é acionado sempre que o usuário clica no componente. O sistema passa o novo valor booleano sugerido (o oposto do valor atual) para esta função. É dentro deste bloco que você deve atualizar a sua variável de estado (`notifyByEmail = it`) para que o Compose redesenhe a interface. Se você passar `null` para este parâmetro, o Checkbox se tornará não interativo, mas ainda manterá sua aparência habilitada.
    
- **modifier (Modifier):** Utilizado para ajustes de layout externos ao comportamento do checkbox. No exemplo acima, o `Modifier` foi aplicado na `Row` pai para garantir que o clique em qualquer lugar da linha alterne o estado do Checkbox, aumentando a usabilidade e a acessibilidade (seguindo as diretrizes de que áreas de toque devem ter no mínimo 48.dp).
    
- **enabled (Boolean):** Define se o componente está ativo para interação. Quando definido como `false`, o Checkbox não responde a cliques e assume uma tonalidade visual acinzentada (esmaecida). Isso é útil para formulários onde uma opção depende da marcação de outra anterior.
    
- **colors (CheckboxColors):** Permite a customização técnica das cores do componente em seus diversos estados. Através de `CheckboxDefaults.colors()`, é possível definir:
    
    - `checkedColor`: A cor do preenchimento quando marcado.
        
    - `uncheckedColor`: A cor da borda quando desmarcado.
        
    - `checkmarkColor`: A cor do ícone de "v" (check) dentro do quadrado.
        
    - `disabledCheckedColor`: A cor que o componente assume se estiver marcado, mas desabilitado.
        
- **interactionSource (MutableInteractionSource):** É uma propriedade avançada que representa o fluxo de interações do componente (como pressões, focos ou arrastos). Ela permite que você crie efeitos visuais personalizados ou reaja a eventos de interação específicos sem necessariamente alterar o estado binário do Checkbox.
    

## Consideração sobre o TriStateCheckbox

Existe ainda uma variação chamada **TriStateCheckbox**. Ela possui a propriedade `state` em vez de `checked`, aceitando o tipo `ToggleableState`. Os valores possíveis são `On`, `Off` e `Indeterminate`. Esta versão é tecnicamente utilizada quando o Checkbox principal controla um grupo de sub-itens e apenas uma parte deles está marcada.

Deseja que eu explique como implementar a lógica de um Checkbox "Mestre" que marca e desmarca todos os outros de uma lista?