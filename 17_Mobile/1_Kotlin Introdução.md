


---

O Kotlin foi desenvolvido para ter 100% de **interoperabilidade** com Java. Isso significa que:
- Você pode chamar uma classe Java dentro de um arquivo Kotlin.
- Você pode usar uma biblioteca Kotlin dentro de um projeto Java.    

![500](../attachments/Pasted%20image%2020260303133323.png)
### **1. Sintaxe básica**

Main
![](../attachments/Pasted%20image%2020260303140906.png)

Variáveis
![](../attachments/Pasted%20image%2020260303140745.png)

Funções
![](../attachments/Pasted%20image%2020260303145317.png)

When é o switch case evoluido
![](../attachments/Pasted%20image%2020260303150727.png)
![](../attachments/Pasted%20image%2020260303150835.png)

For
![](../attachments/Pasted%20image%2020260303151103.png)
![](../attachments/Pasted%20image%2020260303151134.png)


Em Kotlin as variáveis não podem ser nulas. 
- **`nome: String?`**: Diz que pode ter um texto OU ser nula.
- `nomeVariável?` : Se for nulo, não faz nada e retorna null. Se NÃO for nulo, deixa você acessar a propriedade ou o método.
- O `!!` é a forma de você dizer ao compilador: **"Eu tenho certeza absoluta que essa variável não é nula"**

O `.let` é uma "função de escopo". Quando combinado com o operador de chamada segura (?), ele cria um bloco de código que só será executado se a variável não for nula.
![](../attachments/Pasted%20image%2020260303190645.png)

