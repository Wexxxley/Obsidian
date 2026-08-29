
#Concluded 

---
### 1. **interface vs type**

- Utilize a **interface** sempre que precisar definir a estrutura de um objeto. É a ferramenta padrão para modelar entidades de dados e mapear as respostas recebidas de uma API. Se o dado opera como um objeto clássico, a interface deve ser a sua escolha primária.

- Utilize o **type** quando precisar declarar qualquer estrutura que não seja apenas um objeto. Como para criar uniões lógicas (exigir que uma variável aceite um número ou seja null), definir tipos literais específicos (limitar uma var às palavras "aberto" | "fechado").

---
### 2. Criando o TODO
![](../../../attachments/Pasted%20image%2020260828132733.png)
![250](../../../attachments/Pasted%20image%2020260829140737.png)

**App.vue**
![](../../../attachments/Pasted%20image%2020260829172517.png)
- Foi criado o tipo Task, depois criado um estado reativo com uma lista de tasks.
- Foi criado uma propriedade computada Porcentagem que depende do estado reativo Tasks.

**Todo list**![300](../../../attachments/Pasted%20image%2020260828134450.png)É uma casca vazia para receber os lists itens. Por isso o SLOT.

**ListIten**

![](../../../attachments/Pasted%20image%2020260829101348.png)
- O modo de edição baseia-se em uma estrutura de alternância. Somente o input ou o span permanecem visíveis.
- **Quando o input está ativo**: 
	- **blur="endEditing":** O evento blur é disparado no momento em que o elemento perde o foco físico (por exemplo, quando o usuário clica em qualquer outro lugar). 
	- **keydown.enter="endEditing"**:  intercepta o pressionamento da tecla "Enter".  Permitindo que o usuário consolide a edição tanto via mouse quanto via teclado.
- **Quando o span está ativo:**
	- **:class="{ 'is-done': done }"**: adiciona o css para mostrar que foi finalizada. 
    
**ProgressBar**![600](../../../attachments/Pasted%20image%2020260828140010.png)