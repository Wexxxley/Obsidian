
#Concluded 

---
### **1. Event Handlers**

Diferente do HTML nativo (onclick), o React utiliza a convenção camelCase para eventos (onClick, onChange) e espera uma função.

**Implementação no Componente Search:** Define-se uma função handleChange dentro do componente para capturar a interação.
![](../../attachments/Pasted%20image%2020251123193132.png)
- **onChange={handleChange}**: Passa a refere para ser executada quando o evento ocorrer


Nesse exemplo, toda vez que digito algo no input, o console imprime.
![](../../attachments/Pasted%20image%2020251123193353.png)

---
### **2. React Props**

As Props são o <mark style="background: #ADCCFFA6;">mecanismo para passar dados de um componente pai para um componente filho</mark>. Props são **imutáveis**. Um componente filho nunca deve alterar as props recebidas. Elas servem estritamente para o fluxo de dados unidirecional (top-down) .

**Refatoração da Lista:** A variável stories (anteriormente list) é movida para o escopo do componente `App` e passada para o componente `List` via atributo.
![](../../attachments/Pasted%20image%2020251123194538.png)

**Recebendo Props:** O componente filho recebe um objeto `props` como primeiro argumento da função. As propriedades passadas no JSX tornam-se chaves desse objeto.
![](../../attachments/Pasted%20image%2020251123194555.png)

