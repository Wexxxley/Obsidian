
#Concluded 

---
### **1. Switch**

O Switch é um componente de seleção binária. Ele é composto fundamentalmente por dois parâmetros obrigatórios:
- **checked:** Um booleano que define o estado visual atual do componente na interface.
- **onCheckedChange:** Uma função de retorno (callback) que é disparada quando o usuário interage com o interruptor, devolvendo o novo valor booleano.

Para que o switch funcione dinamicamente, é necessário criar uma variável de estado 

**Exemplo remoção condicional:** A limitação é que quando o componente é removido, os elementos abaixo dele "sobem" para ocupar o espaço vazio, alterando o layout.
![530](../../../../attachments/Pasted%20image%2020260320080929.png)
![250](../../../../attachments/switch.gif)



**Propriedade Alpha:** Em vez de remover o componente, utiliza-se o modificador. O componente continua existindo no layout e ocupando seu espaço original.
![530](../../../../attachments/Pasted%20image%2020260320081331.png)
![300](../../../../attachments/switch2.gif)


---
### **2. Dropdown menu**

O componente permite que o usuário selecione um item de uma lista suspensa para realizar ações ou preencher campos. O menu não é um componente único, mas uma combinação de elementos que trabalham juntos:

- **Box:** Utilizado como contêiner principal.
- **Row/Text/Image:** Servem como o "gatilho" visual que o usuário clica para abrir a lista.
- **DropDownMenu:** O componente que contém a lista suspensa.
- **DropdownMenuItem:** Cada opção individual dentro do menu.

O componente depende de dois estados principais para funcionar:
- **expanded (Boolean):** Controla a visibilidade do menu.
- **onDismissRequest:** Um _callback_ acionado quando o usuário clica fora do menu ou pressiona o botão voltar. 

![580](../../../../attachments/Pasted%20image%2020260320083512.png)
![300](../../../../attachments/dropdown.gif)

- **Rolagem Automática:** Se a lista for muito longa, o DropdownMenu cria automaticamente uma barra de rolagem interna.
