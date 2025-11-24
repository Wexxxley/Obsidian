
#Concluded 

---
### **1. Event Handlers**

Para adicionar interatividade, o React utiliza **Event Handlers**.  Diferente do HTML nativo (onclick), o React utiliza a convenção camelCase para eventos (onClick, onChange) e espera uma função.

**Implementação no Componente Search:** Define-se uma função handleChange dentro do componente para capturar a interação.
![](../../attachments/Pasted%20image%2020251123193132.png)
Deve-se passar a referência da função, não a sua execução.
- **Correto:** onChange={handleChange}. Passa a func para ser executada quando o evento ocorrer
- **Incorreto:** onChange={handleChange()}. Executa a função durante a renderização.

Nesse exemplo, toda vez que digito algo no input, o console imprime.
![](../../attachments/Pasted%20image%2020251123193353.png)

---
### **2. React Props**

As Props são o mecanismo para passar dados de um componente pai para um componente filho.

- Props são **imutáveis**. Um componente filho nunca deve alterar as props recebidas. Elas servem estritamente para o fluxo de dados unidirecional (top-down) .

**Refatoração da Lista:** A variável stories (anteriormente list) é movida para o escopo do componente `App` e passada para o componente `List` via atributo JSX.`
![](../../attachments/Pasted%20image%2020251123194538.png)

**Recebendo Props:** O componente filho recebe um objeto `props` como primeiro argumento da função. As propriedades passadas no JSX tornam-se chaves desse objeto.
![](../../attachments/Pasted%20image%2020251123194555.png)

---

