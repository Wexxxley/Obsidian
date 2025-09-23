

---
### **1. Princípio da Substituição de Liskov (LSP)**.
Você está desenvolvendo um sistema de fidelidade onde diferentes tipos de clientes recebem recompensas após uma compra. O sistema utiliza o conceito de polimorfismo, mas a hierarquia atual viola o **Princípio da Substituição de Liskov (LSP)**.

A regra é: um `ClienteEspecial` (subclasse) deve poder substituir o `ClientePadrao` (superclasse) sem alterar o comportamento esperado do programa principal.

O código inicial define um método `calcular_recompensa` em `ClientePadrao` que, para simplificar, sempre calcula um valor. No entanto, o `ClienteEspecial` **lança uma exceção** se a compra for muito pequena, ou seja, ele muda o comportamento fundamental do método base, quebrando a expectativa de quem chama o código.

**Sua tarefa é refatorar o código para:**
1. **Resolver a violação do LSP:** Garanta que o método `calcular_recompensa` funcione para qualquer subclasse. 
2. **Aplicar "Tell, Don't Ask" (Calisthenics):** Remova o uso de `get_valor` no método de recompensa, forçando o cálculo a ocorrer **dentro** da classe que possui os dados da compra.

---
### **2. Open/Closed Principle (OCP) em Geração de Relatórios:**

Um sistema de alunos precisa gerar relatórios em diferentes formatos (CSV, HTML, PDF).
A ideia é forçar o uso de uma interface `GeradorDeRelatorio` para que um novo formato (ex: JSON) possa ser adicionado sem modificar a classe principal `SistemaDeAlunos`.

---
### **3. Interface Segregation Principle (ISP) em Funcionários de Logística:**

Uma interface `Funcionario` com métodos como ....

A ideia é mostrar que um `Estagiário` não precisa implementar os métodos ... A interface deve ser quebrada em.

### **4. Dependency Inversion Principle (DIP) em Notificações:**

Um `ProcessadorDePedido` envia uma notificação de conclusão usando uma classe concreta `EmailService`.

A ideia é introduzir a interface `INotificador`. Fazer o `ProcessadorDePedido` depender de `INotificador` para que ele possa usar `SmsService` ou `PushService` sem mudanças.