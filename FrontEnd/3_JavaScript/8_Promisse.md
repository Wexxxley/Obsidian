
---

Promisse é um objeto que representa o sucesso ou uma falha de uma operação assíncrona. Normalmente só consumimos uma promisse de terceiros como quando acessamos apis.

![[Pasted image 20250609155006.png]]
![[Pasted image 20250609155023.png]]
- O resto do código é executado enquanto espera o retorno da promessa.
- O construtor `Promise` recebe uma **função executora** como argumento. Esta função executora, por sua vez, recebe dois argumentos: `resolve` e `reject`.
	1. `resolve`: É uma função que você deve chamar quando a operação assíncrona for concluída com **sucesso**. 
	2. `reject`: É uma função que você deve chamar quando a operação assíncrona **falhar**. 
- **setTimeOut** está simulando uma operação assíncrona. `setTimeout` é uma função que agenda a execução de uma função (o primeiro argumento) após um determinado atraso (o segundo argumento, em milissegundos).
- O método `.then()` é anexado à Promise retornada por `getData()` para acessor a valor em caso de sucesso.
- O método `.catch()` é anexado à Promise.
    - O callback `error => console.log(error)` seria executado **somente** se a Promise fosse rejeitada (ou seja, se `reject()` fosse chamado dentro de `getData()` em vez de `resolve()`).
    - O argumento `error` deste callback receberia o valor que foi passado para `reject()` (neste caso, a string `"erro"` se estivesse ativa).