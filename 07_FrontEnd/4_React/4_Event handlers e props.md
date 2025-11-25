
#Concluded 

---
### **1. Event Handlers**

Diferente do HTML nativo (onclick), o React utiliza a convenção camelCase para eventos (onClick, onChange) e espera uma função.

**Implementação no Componente Search:** Define-se uma função handleChange dentro do componente para capturar a interação.
![](../../attachments/Pasted%20image%2020251123193132.png)
- **onChange={handleChange}**: Passa a referência da função para ser executada quando o evento ocorrer. Não passe handleChange() poiss isso executaria a função de cara.

Nesse exemplo, toda vez que digito algo no input, o console imprime.
![](../../attachments/Pasted%20image%2020251123193353.png)

---
### **2. React Props**

As Props são o <mark style="background: #ADCCFFA6;">mecanismo para passar dados de um componente pai para um componente filho</mark>. Props são **imutáveis**. Um componente filho nunca deve alterar as props recebidas.

**Refatoração da Lista:** A variável stories (anteriormente list) é movida para o escopo do componente `App` e passada para o componente `List` via atributo.
![](../../attachments/Pasted%20image%2020251123194538.png)

**Recebendo Props:** O componente filho recebe um objeto `props`.
![](../../attachments/Pasted%20image%2020251123194555.png)

**Desestruturação**
A desestruturação de objetos permite extrair propriedades de um objeto diretamente para variáveis. Em vez de acessar props dentro da função, desestruturamos o objeto diretamente na assinatura da função. Isso torna explícito quais dados o componente requer para funcionar.
![](../../attachments/Pasted%20image%2020251124140417.png)
Isso elimina a necessidade de usar `props.` em todo lugar.
