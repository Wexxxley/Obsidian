

---
### **1. Descrição do Problema**
Você está desenvolvendo um sistema de fidelidade onde diferentes tipos de clientes recebem recompensas após uma compra. O sistema utiliza o conceito de polimorfismo, mas a hierarquia atual viola o **Princípio da Substituição de Liskov (LSP)**.

A regra é: um `ClienteEspecial` (subclasse) deve poder substituir o `ClientePadrao` (superclasse) sem alterar o comportamento esperado do programa principal.

O código inicial define um método `calcular_recompensa` em `ClientePadrao` que, para simplificar, sempre calcula um valor. No entanto, o `ClienteEspecial` **lança uma exceção** se a compra for muito pequena, ou seja, ele muda o comportamento fundamental do método base, quebrando a expectativa de quem chama o código.

**Sua tarefa é refatorar o código para:**
1. **Resolver a violação do LSP:** Garanta que o método `calcular_recompensa` funcione para qualquer subclasse. 
2. **Aplicar "Tell, Don't Ask" (Calisthenics):** Remova o uso de `get_valor` no método de recompensa, forçando o cálculo a ocorrer **dentro** da classe que possui os dados da compra.

---
### **1. Open/Closed Principle (OCP) em Geração de Relatórios:**

Um sistema de alunos precisa gerar relatórios em diferentes formatos (CSV, HTML, PDF. JSON).
        
A ideia é forçar o uso de uma interface `GeradorDeRelatorio` para que um novo formato (ex: JSON) possa ser adicionado sem modificar a classe principal `SistemaDeAlunos`.
        
4. **Interface Segregation Principle (ISP) em Funcionários de Logística:**
    
    - **Contexto:** Uma interface `Trabalhador` com métodos como `dirigirCaminhao()`, `gerenciarEstoque()`, `atenderTelefone()`.
        
    - **Foco:** Mostrar que um `Estagiário` não precisa implementar `dirigirCaminhao()`. A interface deve ser quebrada em `IDirigivel`, `IGerenciavel`, `IAtendivel`.
        
5. **Dependency Inversion Principle (DIP) em Notificações:**
    
    - **Contexto:** Um `ProcessadorDePedido` envia uma notificação de conclusão usando uma classe concreta `EmailService`.
        
    - **Foco:** Introduzir a interface `INotificador`. Fazer o `ProcessadorDePedido` depender de `INotificador` para que ele possa usar `SmsService` ou `PushService` sem mudanças.