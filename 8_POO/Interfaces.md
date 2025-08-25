
---
Uma interface é um **CONTRATO** que define um conjunto de métodos que uma classe deve implementar. Em termos mais simples, a interface diz: "Se você quiser ser do meu tipo, precisa implementar os métodos X, Y e Z."
### **1. Exemplo ilustrativo**
Neste exemplo, temos um sistema de controle de um banco. Queremos que Diretor, Gerente e Cliente sejam autenticaveis no meu sistema.

A forma abaixo é inadequada, pois
1. Se um `Engenheiro` também precisar se autenticar no futuro? Seria necessário mudar sua herança de `Funcionario` para `FuncionarioAutenticavel`.
2. A classe `Cliente` também precisa se autenticar, mas ela não é um `Funcionario`. 
![](attachments/Pasted%20image%2020250825092255.png)

No exemplo abaixo, em vez de uma classe, foi criada uma interface chamada `Autenticavel`. Ela representa uma capacidade do tipo "**sabe ou pode fazer"** . Agora, qualquer classe que precise ter a capacidade de se autenticar simplesmente implementa a interface.
1. Se um `Engenheiro` precisar se autenticar, basta que a classe `Engenheiro` implemente a interface.
2. O sistema pode agora tratar qualquer objeto simplesmente como um `Autenticavel`, permitindo que o mecanismo de login funcione para todos.
![650](attachments/Pasted%20image%2020250825092213.png)

A comparação entre os dois diagramas ilustra uma lição: "**use herança para modelar o que um objeto "é" e use interfaces para modelar o que um objeto "pode fazer"**. 

---
### **2. Por que e quando usar interfaces?**

#### **2.1 Abstração e Flexibilidade**
A interface ajuda a focar no "o quê" um objeto faz, em vez de no "como" ele faz. 

**Exemplo:** Imagine um sistema de e-commerce que precisa processar pagamentos. Hoje, a empresa pode usar o Pix, mas amanhã pode decidir adicionar o PayPal ou até mesmo um sistema de pagamento próprio.
- **Sem Interfaces**: Você teria um código cheio de if/else ou dependências  para cada processador de pagamento, o que torna o código difícil de modificar. Cada vez que um novo provedor for adicionado, você precisa alterar o código central que processa os pagamentos.
- **Com Interfaces**: Você cria uma interface `ProcessadorDePagamento` que define: ` processarPagamento(double valor, Pagamento detalhes)` . As classes `PixGateway` e `PaypalGateway` simplesmente implementam essa interface. O restante do seu sistema não se importa se o pagamento está sendo processado pelo Pix ou pelo PayPal, pois ele trabalha apenas com a interface . 

#### **2.2 Múltipla Herança**
Java não permite que uma classe herde de múltiplas classes, mas permite que ela **implemente múltiplas interfaces**. Isso é útil para dar a uma classe várias capacidades. 

**Exemplo:** Em uma empresa, existe a classe `Funcionario`, mas diferentes cargos têm habilidades distintas que não se encaixam em uma única hierarquia. Um `Vendedor` e um `Gerente` podem ter a habilidade de `EmitirRelatorio`, mas apenas o `Gerente` pode `AprovarOrcamento`. 
#### **2.3 Padrões de Projeto**
Interfaces são essenciais para a maioria dos padrões de projeto. 
#### **2.4 Manutenção**
Ao usar interfaces, você programa para a "interface" e não para a "implementação". Isso significa que você pode trocar uma classe por outra que implementa a mesma interface sem afetar o resto do código. Isso facilita a **manutenção** e o **crescimento** do projeto.

**Exemplo:** Voltando ao exemplo do processamento de pagamentos. Seu sistema foi construído para usar a interface `ProcessadorDePagamento`. Agora, imagine que a empresa fecha um acordo com um novo provedor chamado "SecurePay" e precisa migrar o processamento de pagamentos. Como o sistema não está vinculado à implementação específoca, a mudança é simples. Você simplesmente cria uma nova classe `SecurePayGateway` que implementa a interface `ProcessadorDePagamento`. Isso é um benefício enorme, pois a mudança de uma tecnologia não gera um efeito dominó de alterações por todo o código.

---
### **3. Exemplo prático: ProcessadorDePagamento**

Primeiro, definimos a interface **`ProcessadorDePagamento`**. Ela é o contrato que todos os gateways de pagamento devem seguir. O método `processarPagamento` é o único requisito.

```java
public interface ProcessadorDePagamento {
    void processarPagamento(double valor);
}
```

Agora, criamos classes que implementam o contrato `ProcessadorDePagamento`, cada uma com sua própria lógica de processamento.

```java
// Gateway de Pagamento para Pix
public class PixGateway implements ProcessadorDePagamento {
    @Override
    public void processarPagamento(double valor) {
        System.out.println("Processando pagamento de R$" + valor + " via Pix.");
    }
}

// Gateway de Pagamento para PayPal
public class PaypalGateway implements ProcessadorDePagamento {
    @Override
    public void processarPagamento(double valor) {
        System.out.println("Processando pagamento de R$" + valor + " via PayPal.");
    }
}

// Gateway de Pagamento para Stripe
public class StripeGateway implements ProcessadorDePagamento {
    @Override
    public void processarPagamento(double valor) {
        System.out.println("Processando pagamento de R$" + valor + " via Stripe.");
    }
}
```

---

### O Serviço Principal (O Código "Brincável")

A classe `ServicoDePedidos` representa a lógica central do seu sistema. Ela não depende de um gateway específico, apenas do contrato `ProcessadorDePagamento`.

Java

```java
public class ServicoDePedidos {

    private ProcessadorDePagamento processador;

    // O construtor recebe qualquer objeto que seja um ProcessadorDePagamento
    public ServicoDePedidos(ProcessadorDePagamento processador) {
        this.processador = processador;
    }

    public void finalizarCompra(double valor) {
        System.out.println("Iniciando finalização da compra...");
        this.processador.processarPagamento(valor);
        System.out.println("Compra finalizada com sucesso!");
    }
}
```


### A Brincadeira Começa!

No seu `main` (a parte que você pode "brincar"), você verá a flexibilidade em ação. Você pode facilmente trocar o `ProcessadorDePagamento` que o `ServicoDePedidos` utiliza.

Java

```java
public class Main {
    public static void main(String[] args) {
        // Cenário 1: Finalizar uma compra usando o Pix
        System.out.println("--- COMPRANDO COM PIX ---");
        ProcessadorDePagamento pixProcessor = new PixGateway();
        ServicoDePedidos servicoComPix = new ServicoDePedidos(pixProcessor);
        servicoComPix.finalizarCompra(150.00);

        System.out.println("\n--- MUDANDO PARA PAYPAL ---");
        // Cenário 2: Mudar para o PayPal é fácil, só precisa de uma nova instância
        ProcessadorDePagamento paypalProcessor = new PaypalGateway();
        ServicoDePedidos servicoComPaypal = new ServicoDePedidos(paypalProcessor);
        servicoComPaypal.finalizarCompra(250.75);

        System.out.println("\n--- MUDANDO PARA STRIPE ---");
        // Cenário 3: Mudar para o Stripe é igualmente simples
        ProcessadorDePagamento stripeProcessor = new StripeGateway();
        ServicoDePedidos servicoComStripe = new ServicoDePedidos(stripeProcessor);
        servicoComStripe.finalizarCompra(50.50);
    }
}
```

