
#Concluded 

---
O Compose não lê o banco de dados sozinho; ele precisa que o ViewModel entregue os dados em um formato que ele entenda (Estado), e para criar esse ViewModel com parâmetros, precisamos da Factory.
### 1. ViewModelFactory

Se o `NoteViewModel` não tivesse parâmetros no construtor, o sistema saberia criá-lo . Porém, como ele precisa do `NoteRepository`, o sistema não sabe de onde tirar esse repositório. A **Factory** é um padrão de projeto que serve como um manual de instruções para criar objetos.

No mesmo arquivo NoteViewModel
![](../../../../attachments/Pasted%20image%2020260331135141.png)

![](../../../../attachments/Pasted%20image%2020260409062643.png)
