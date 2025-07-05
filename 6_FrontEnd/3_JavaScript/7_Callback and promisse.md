
---
### **1. Callback**
A callback is a function passed as an argument to another function.
![Pasted image 20250609150854](../../attachments/Pasted%20image%2020250609150854.png)
- In the example above,  ==(x) => x >= 0== this a **callback function**.

---
### **2. Promisse**
Promisse é um objeto que **representa sucesso ou falha de uma operação assíncrona** Normalmente só consumimos uma promisse de terceiros, como quando acessamos apis, banco de dados e etc.
![Pasted image 20250609155006](../../attachments/Pasted%20image%2020250609155006.png)
![Pasted image 20250609155023](../../attachments/Pasted%20image%2020250609155023.png)
- O resto do código é executado enquanto espera o retorno da promessa.
- O construtor `Promise` recebe uma **função** como argumento. Esta função, por sua vez, recebe dois argumentos: `resolve` e `reject`.
	1. `resolve`: É uma função que você deve chamar quando a operação assíncrona for concluída com **sucesso**. 
	2. `reject`: É uma função que você deve chamar quando a operação assíncrona **falhar**. 
- `setTimeout` é uma função que agenda a execução de uma função após um determinado atraso.
- O método `.then()` é anexado à Promise retornada por `getData()` para acessor a valor em caso de sucesso.
- O método `.catch()` é anexado à Promise para acessor o retorno e mcaso de fracasso.

