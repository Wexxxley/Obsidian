

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
