
---
Uma interface é um **CONTRATO** que define um conjunto de métodos que uma classe deve implementar. Em termos mais simples, a interface diz: "Se você quiser ser do meu tipo, precisa implementar os métodos X, Y e Z."
### **1. Exemplo ilustrativo**
Neste exemplo, temos um sistema de controle de um banco. Queremos que Diretor, Gerente e Cliente sejam autenticaveis no meu sistema.

A forma abaixo é inadequada, pois
1. Se um `Engenheiro` também precisar se autenticar no futuro? Seria necessário mudar sua herança de `Funcionario` para `FuncionarioAutenticavel`.
2. A classe `Cliente` também precisa se autenticar, mas ela não é um `Funcionario`. 
![](../attachments/Pasted%20image%2020250825092255.png)

No exemplo abaixo, em vez de uma classe, foi criada uma interface chamada `Autenticavel`. Ela representa uma capacidade do tipo "**sabe ou pode fazer"** . Agora, qualquer classe que precise ter a capacidade de se autenticar simplesmente implementa a interface.
1. Se um `Engenheiro` precisar se autenticar, basta que a classe `Engenheiro` implemente a interface.
2. O sistema pode agora tratar qualquer objeto simplesmente como um `Autenticavel`, permitindo que o mecanismo de login funcione para todos.
![650](../attachments/Pasted%20image%2020250825092213.png)

A comparação entre os dois diagramas ilustra uma lição: "**use herança para modelar o que um objeto "é" e use interfaces para modelar o que um objeto "pode fazer"**. 

---
### **2. Por que e quando usar interfaces?**

#### **2.1 Abstração e Flexibilidade**
**Exemplo:** Imagine um sistema de e-commerce que precisa processar pagamentos. Hoje, a empresa pode usar o Pix, mas amanhã pode decidir adicionar o PayPal ou até mesmo um sistema de pagamento próprio.
- **Sem Interfaces**: Você teria um código cheio de if/else ou dependências  para cada processador de pagamento, o que torna o código difícil de modificar. Cada vez que um novo provedor for adicionado, você precisa alterar o código central que processa os pagamentos.
- **Com Interfaces**: Você cria uma interface `ProcessadorDePagamento` que define: ` processarPagamento(double valor, Pagamento detalhes)` . As classes `PixGateway` e `PaypalGateway` simplesmente implementam essa interface. O restante do seu sistema não se importa se o pagamento está sendo processado pelo Pix ou pelo PayPal, pois ele trabalha apenas com a interface . 

#### **2.2 Múltipla Herança**
Java não permite que uma classe herde de múltiplas classes, mas permite que ela **implemente múltiplas interfaces**. Isso é útil para dar a uma classe várias capacidades. 
#### **2.3 Padrões de Projeto**
Interfaces são essenciais para a maioria dos padrões de projeto. 
#### **2.4 Manutenção**
Ao usar interfaces, você programa para a "interface" e não para a "implementação". Isso significa que você pode trocar uma classe por outra que implementa a mesma interface sem afetar o resto do código. Isso facilita a **manutenção** do projeto.

---
### **3. Exemplo prático: ProcessadorDePagamento**

Primeiro, definimos a interface **`ProcessadorDePagamento`**. Ela é o contrato que todos os gateways de pagamento devem seguir. O método `processarPagamento` é o único requisito.

![](../attachments/Pasted%20image%2020250825143122.png)

Agora, criamos classes que implementam o contrato `ProcessadorDePagamento`, cada uma com sua própria lógica de processamento.
![](../attachments/Pasted%20image%2020250825143136.png)
![](../attachments/Pasted%20image%2020250825143148.png)
