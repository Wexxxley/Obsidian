
#Concluded 

---
### **1. Event Handlers**

Diferente do HTML nativo (onclick), o React utiliza a convenção camelCase para eventos (onClick, onChange) e espera uma função.

**Implementação no Componente Search:** Define-se uma função handleChange dentro do componente para capturar a interação.
![](../../../../attachments/Pasted%20image%2020251123193132.png)
- **onChange={handleChange}**: Passa a referência da função para ser executada quando o evento ocorrer. 

Nesse exemplo, toda vez que digito algo no input, o console imprime.
![](../../../../attachments/Pasted%20image%2020251123193353.png)

---
### **2. React Props**

As Props são o <mark style="background: #ADCCFFA6;">mecanismo para passar dados de um componente pai para um componente filho</mark>. Props são **imutáveis**. Um componente filho nunca deve alterar as props recebidas.

Como as _props_ frequentemente contêm referências na memória para objetos originados no escopo do componente pai, uma mutação interna no filho afetaria diretamente os dados externos. O React exige que oo componentes devem processar a renderização sem causar efeitos colaterais (_side effects_) no escopo externo. Mudanças dinâmicas na interface devem ser gerenciadas via _State_.

**Refatoração da Lista:** A variável stories (anteriormente list) é movida para o escopo do componente `App` e passada para o componente `List` via atributo.
![](../../../../attachments/Pasted%20image%2020251123194538.png)

**Recebendo Props:** O componente filho recebe um objeto `props`.
![](../../../../attachments/Pasted%20image%2020251123194555.png)

**Desestruturação**: A desestruturação de objetos permite extrair propriedades de um objeto diretamente para variáveis. Em vez de acessar props dentro da função, desestruturamos o objeto diretamente na assinatura da função.
![](../../../../attachments/Pasted%20image%2020251124140417.png)

O React impõe o chamado fluxo de dados unidirecional (_one-way data flow_). Isso significa que as informações trafegam estruturalmente em uma direção exclusiva: de pai para filho. Não existe propagação inversa natural via props.
![500](../../../../attachments/Pasted%20image%2020260513064218.png)