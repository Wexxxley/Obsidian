

---
### 1. **interface vs type**

- Utilize a **interface** sempre que precisar definir a estrutura de um objeto. É a ferramenta padrão para modelar entidades de dados, mapear as respostas recebidas de uma API ou estruturar as propriedades (`Props`) de um componente. Se o dado transita e opera puramente como um objeto clássico, a `interface` deve ser a sua escolha primária.

### O momento de usar `type`

Utilize o `type` obrigatoriamente quando precisar declarar qualquer estrutura que **não seja apenas um objeto**. O seu uso é exigido tecnicamente para criar uniões lógicas (exigir que uma variável aceite um número ou seja `null`), definir tipos literais específicos (como limitar uma variável estritamente às palavras `"aberto" | "fechado"`) ou criar apelidos rápidos para tipos primitivos e matrizes fechadas.

---
### 2. Criando o TODO
![](../../../attachments/Pasted%20image%2020260828132733.png)
**App.vue**
![](../../../attachments/Pasted%20image%2020260828134410.png)
- Foi criado o tipo Task, depois criado um estado reativo com uma lista de tasks.
- Foi criado uma propriedade computada Porcentagem que depende do estado reativo Tasks.

**Todo list**![300](../../../attachments/Pasted%20image%2020260828134450.png)É uma casca vazia para receber os lists itens. Por isso o SLOT.

**ListIten**![](../../../attachments/Pasted%20image%2020260828135329.png)
**ProgressBar**![600](../../../attachments/Pasted%20image%2020260828140010.png)