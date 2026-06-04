
#Concluded 

---
### **1. CheckBox**

O componente Checkbox é para permitir que o usuário selecione uma ou mais opções de um conjunto, ou confirme um estado binário.  O Checkbox depende de uma variável booleana externa.
- **value:** Um parâmetro booleano.
- **onCheckedChange:** Uma função de retorno (callback) disparada sempre que o usuário interage com o componente. 

![](../../../../attachments/Pasted%20image%2020260319181215.png)
![](../../../../attachments/checkBoxSimples.gif)

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

![550](../../../../attachments/Pasted%20image%2020260319212728.png)
![300](../../../../attachments/radioButton.gif)

No exemplo acima, utilizamos `Modifier.selectable` em vez de `.clickable`.
- selectable é otimizado para componentes de seleção única. 

**Checkbox e RadioButton**
- O Checkbox é para múltiplas escolhas independentes. O RadioButton é para uma escolha única obrigatória entre várias.
- Um Checkbox pode ser desmarcado clicando nele novamente. Um RadioButton, por padrão, não é desmarcado ao ser clicado novamente,

