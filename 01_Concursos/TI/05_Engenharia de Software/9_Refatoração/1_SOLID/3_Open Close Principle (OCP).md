
> [!NOTE]
> “As entidades de software (classes, módulos, funções) devem ser abertas para ampliação, mas fechadas para modificação”.  

Quando uma única mudança resulta em uma sucessão de mudanças nos módulos dependentes, o projeto tem um grande problema. O OCP nos aconselha a refatorar o sistema para que alterações não causem mais modificações. Se o OCP for bem aplicado, **mudanças são obtidas pela adição de novo código e não pela alteração de código antigo que já funciona.**

Os módulos que obedecem ao OCP têm duas características principais:
1. **São abertos para ampliação**: À medida que os requisitos do aplicativo mudam, podemos ampliar o módulo com novos comportamentos que satisfaçam essas alterações. 
2. **São fechados para modificação**: Ampliar o comportamento de um módulo não resulta em mudanças no código-fonte. 

---
### **Como modificar os comportamentos de um módulo sem alterar seu código-fonte?**  
 
 Com **abstração**. Em qualquer  linguagem de programação orientada a objetos, é possível criar abstrações fixas e que ainda assim representam um grupo ilimitado de comportamentos possíveis. As abstrações são classes base abstratas e o grupo ilimitado de comportamentos possíveis é representado por todas as classes derivadas possíveis.

 Um modulo que implementa uma abstração pode ser **fechado para modificação**, pois ele depende de uma abstração fixa. Apesar disso, o comportamento desse módulo pode ser **ampliado pela criação de novas derivadas da abstração.**

Imagine que você tem uma classe chamada **`PaymentProcessor`** que lida com pagamentos para sua aplicação de comércio eletrônico. Inicialmente, ela suporta apenas pagamentos com cartão de crédito:

```java
class PaymentProcessor {
    public void processCreditCardPayment() {
        // Código para processar o pagamento com cartão de crédito
    }
}
```

Mais tarde, você decide estender sua aplicação para suportar pagamentos via PayPal. Para fazer isso, você precisa **modificar** a classe **`PaymentProcessor`** existente:

```java
class PaymentProcessor {
    public void processCreditCardPayment() {
        // Código para processar o pagamento com cartão de crédito
    }
    
    public void processPayPalPayment() {
        // Código para processar o pagamento via PayPal
    }
}
```

No primeiro exemplo, você **violou o Princípio Aberto/Fechado** porque teve que **modificar a classe existente** para adicionar suporte a um novo método de pagamento. 

Para aderir ao **Princípio Aberto/Fechado**, você pode usar uma **abstração** e criar classes separadas para cada método de pagamento **sem modificar o código existente**:

```java
interface PaymentProcessing {
    public void processPayment();
}

class CreditCardPaymentProcessor implements PaymentProcessing {
    public void processPayment() {
        // Código para processar o pagamento com cartão de crédito
    } 
}
class PayPalPaymentProcessor implements PaymentProcessing {
    public void processPayment() {
        // Código para processar o pagamento via PayPal
    }
}
```

Com essa abordagem, você introduziu uma abstração, **`PaymentProcessing`**, e criou classes específicas para cada método de pagamento. 
