
#Concluded 

---
### **1. Button**

Tudo o que você coloca dentro do conteudo do botão se comporta como se estivesse dentro de uma Row. Por isso, se você colocar um `Icon` e um `Text`, eles ficarão automaticamente um ao lado do outro.

![](../../../attachments/Pasted%20image%2020260319102931.png)
- **`shape`**: Define o arredondamento.
- **`contentPadding`**: Ajusta o espaçamento interno.
- `border`: Define borda
- `OnClick`: Recebe uma função

Usando estado no botão
![560](../../../attachments/Pasted%20image%2020260319105716.png)
![300](../../../attachments/Peek%202026-03-19%2013-50.gif)
1. **remember:** O Compose redesenha a tela constantemente. O remember serve para o botão não "esquecer" o valor da variável toda vez que a função for executada.
2. **mutableStateOf:** É um tipo de variável especial. O Compose fica "vigiando" essa variável; se o valor dela muda, o Compose entende que teve mudanças.
3. **onClick:** Dentro do clique do botão, você altera o valor dessa variável. Essa mudança avisa o sistema: "Ei, o estado mudou, redesenhe a tela agora!".

--- 
### **2. Estado vs Variável comum**

- **Variável Comum:** Se você altera o valor de uma variável local comum, o valor muda na memória, mas a UI não sabe disso. Ela continua exibindo o valor antigo.
    
- **Variável de Estado:** Quando você altera um estado, o framework detecta essa mudança e dispara automaticamente o processo de Recomposição. 

- **Variável Comum:** Toda vez que a função do componente é executada novamente, a variável comum é reinicializada com seu valor padrão. 
    
- **Variável de Estado:** Através de mecanismos como o remember, o framework reserva um espaço na memória permitindo que o valor seja lembrado.

---
### **3. TextFild**

O TextField é o componente de entrada de texto. O TextField não "guarda" o texto sozinho. Se você digitar e não atualizar o estado, o texto não aparece na tela. 

Para um TextField funcionar, ele precisa de duas coisas obrigatoriamente:
- **value**: O que está escrito nele agora (o Estado).
- **onValueChange**: O que fazer quando o usuário digita uma tecla nova.

![](../../../attachments/Pasted%20image%2020260319140505.png)
- **label**: O texto que "flutua" quando você clica.
- **placeholder**: Dica.
- **leadingIcon /trailingIcon**: Ícones no início ou no fim.
- **visualTransformation**: Usado para esconder a senha: PasswordVisualTransformation().
- **keyboardOptions**: Define o tipo de teclado (apenas números, e-mail, etc).
- **readOnly = true**: O usuário pode selecionar o texto e copiar, mas não pode mudar (bom para datas escolhidas em calendários).

**Remember**: No Compose, as funções são executadas de novo toda vez que algo muda na tela. Se você não usasse o remember, a sua variável seria resetada para o valor inicial toda vez que a tela fosse redesenhada.

**MutableState**: Quando o valor contido nesse estado é alterado, o Compose agenda automaticamente a recomposição de todas as funções que leram esse valor específico.
- **mutableStateOf**: implementação genérica. Ela aceita qualquer tipo de objeto. 
- **mutableIntStateOf**: Uma implementação especializada para valores do tipo `Int`. 
- **mutableFloatStateOf**: Especializada para o tipo `Float`. 
- **mutableStateListOf**: Cria uma lista mutável.

**Simulando uma tela de cadastro**
![500](../../../attachments/Pasted%20image%2020260319144500.png)
![300](../../../attachments/tela%20cadastro.gif)
