
---
### **1. Callback**
A callback is a function passed as an argument to another function.
![Pasted image 20250609150854](../../attachments/Pasted%20image%2020250609150854.png)
- In the example above,  ==(x) => x >= 0== this a **callback function**.

---
### **2. Promisse**
Promisse é um objeto que **representa sucesso ou falha de uma operação assíncrona** Normalmente só consumimos uma promisse de terceiros, como quando acessamos apis, banco de dados e etc.

Nesse exemplo estamos simulando uma operação assíncrona.
![450](../../attachments/Pasted%20image%2020250609155006.png)
![Pasted image 20250609155023](../../attachments/Pasted%20image%2020250609155023.png)
- O resto do código é executado enquanto espera o retorno da promessa.
- O construtor `Promise`recebe um callback. Esta função, por sua vez, recebe dois argumentos: `resolve` e `reject`.
	1. `resolve`: Deve ser chamada quando a operação for concluída com **sucesso**. 
	2. `reject`: Deve ser chamada quando a operação **falhar**. 
- `setTimeout`:  função que agenda a execução de uma função após um determinado tempo.
- O método `.then()` é anexado à Promise retornada para acessor a valor em caso de sucesso.
- O método `.catch()` é anexado à Promise para acessar o retorno em caso de fracasso.

