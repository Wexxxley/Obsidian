

FOCO no **Liskov Substitution Principle (LSP)** e na regra do Calisthenics Evite Getters/Setters

### Descrição do Problema
Você está desenvolvendo um sistema de fidelidade onde diferentes tipos de clientes recebem recompensas após uma compra. O sistema utiliza o conceito de polimorfismo, mas a hierarquia atual viola o **Princípio da Substituição de Liskov (LSP)**.

A regra é: um `ClienteEspecial` (subclasse) deve poder substituir o `ClientePadrao` (superclasse) sem alterar o comportamento esperado do programa principal.

#### O Problema de Design
O código inicial define um método `calcular_recompensa` em `ClientePadrao` que, para simplificar, sempre calcula um valor. No entanto, o `ClienteEspecial` **lança uma exceção** se a compra for muito pequena, ou seja, ele muda o comportamento fundamental do método base, quebrando a expectativa de quem chama o código.

**Sua tarefa é refatorar o código para:**

1. **Resolver a violação do LSP:** Garanta que o método `calcular_recompensa` funcione para qualquer subclasse sem lançar exceções inesperadas ou quebrar o contrato da superclasse. O cálculo deve sempre retornar um valor ou zero, e a validação deve ser movida.
    
2. **Aplicar "Tell, Don't Ask" (Calisthenics):** Remova o uso de `get_valor` no método de recompensa, forçando o cálculo a ocorrer **dentro** da classe que possui os dados da compra.
    

### Estrutura do Código e Implementação

Aqui estão as classes de modelo a serem refatoradas (o aluno deve corrigir as classes `Compra`, `ClientePadrao` e `ClienteEspecial`):

Java

```java
import java.util.*;

// DEL!
/*
class Compra {
    // Código original com getter
    public double get_valor() { return this.valor; }
}

class ClientePadrao {
    // Código original com problema de contrato
    public double calcular_recompensa(Compra compra) {
        return compra.get_valor() * 0.05;
    }
}
*/
// ADD!

/**
 * CLASSE 1: Compra - Aplicação do "Tell, Don't Ask"
 * Não deve ter um getter para o valor. O cálculo deve ser passado para ela.
 */
class Compra {
    private double valor;

    public Compra(double valor) {
        this.valor = valor;
    }

    // Método que permite a compra saber o próprio valor e aplicá-lo a uma taxa.
    // O Cliente envia a taxa (o que fazer) e não pergunta o valor (get_valor).
    public double aplicar_taxa_de_recompensa(double taxa) {
        return this.valor * taxa;
    }
}

/**
 * CLASSE 2: ClientePadrao - O Contrato (Superclasse)
 * O método calcular_recompensa não deve mudar o contrato.
 */
class ClientePadrao {
    protected final double TAXA_BASE = 0.05;

    // Método de contrato: deve sempre retornar um valor, sem lançar exceções de lógica de negócio.
    public double calcular_recompensa(Compra compra) {
        // Usa o TELL, não o ASK (Calisthenics)
        return compra.aplicar_taxa_de_recompensa(TAXA_BASE);
    }
}

/**
 * CLASSE 3: ClienteEspecial - A Subclasse que deve respeitar o LSP
 * Garante que o método não quebre o programa se substituir o ClientePadrao.
 */
class ClienteEspecial extends ClientePadrao {
    private final double TAXA_ESPECIAL = 0.10;
    private final double MINIMO_PARA_RECOMPENSA = 50.0;

    @Override
    public double calcular_recompensa(Compra compra) {
        // A validação de negócio deve ser suave e retornar 0.0 se não cumprir o requisito,
        // em vez de lançar uma exceção. Isso respeita o LSP.
        
        // Para aplicar a validação sem "Ask" (pedir o valor da compra),
        // o ClienteEspecial precisa de um método privado ou protegido na Compra,
        // OU a lógica de validação do valor mínimo deve ser movida para a Compra.
        // Vamos usar um método auxiliar na Compra para respeitar o TELL, DON'T ASK.
        
        if (!compra.eh_elegivel_para_recompensa_especial(MINIMO_PARA_RECOMPENSA)) {
            System.out.println("info: Compra abaixo do mínimo. Recompensa zerada.");
            return 0.0;
        }

        return compra.aplicar_taxa_de_recompensa(TAXA_ESPECIAL);
    }
}
// ADD!
```

### Ajustes na Classe `Compra` para o LSP

Para que o `ClienteEspecial` possa validar se o valor mínimo foi atingido sem usar um `get_valor` (violando "Tell, Don't Ask"), a responsabilidade de verificar a elegibilidade também deve ser movida para `Compra`.

**Adicione este método à classe `Compra` na solução do aluno:**

Java

```
// Dentro da classe Compra:
    public boolean eh_elegivel_para_recompensa_especial(double minimo) {
        return this.valor >= minimo; // A Compra verifica seu próprio valor
    }
```

### Classe Shell (Interface de Teste)

O `Shell` deve demonstrar que o código principal pode usar o `ClienteEspecial` (subclasse) no lugar do `ClientePadrao` (superclasse) sem quebrar o fluxo.

Java

```java
// O Shell será a interface de teste
public class Shell {
        
        public static void main(String[] a) {
            Scanner scanner = new Scanner(System.in);
            
            // DEL!
            ClientePadrao cliente = new ClientePadrao();
            // ADD!
            
            while (true) {
                var line = scanner.nextLine();
                System.out.println("$" + line);

                var par = line.split(" ");
                var cmd = par[0];

                if (cmd.equals("end")) {
                    break;
                }
                else if (cmd.equals("init_padrao")) {
                    // INSTANCIA O CLIENTE PADRÃO
                    // DEL!
                    cliente = new ClientePadrao();
                    System.out.println("ok");
                } 
                else if (cmd.equals("init_especial")) {
                    // INSTANCIA O CLIENTE ESPECIAL (LSP: PODE SUBSTITUIR O PADRÃO)
                    // DEL!
                    cliente = new ClienteEspecial();
                    System.out.println("ok");
                } 
                else if (cmd.equals("recompensa")) {
                    // CALCULA RECOMPENSA PARA A COMPRA DADA
                    // COM!
                    double valor_compra = Double.parseDouble(par[1]);
                    // DEL!
                    Compra compra = new Compra(valor_compra);
                    double recompensa = cliente.calcular_recompensa(compra);
                    System.out.printf("recompensa: %.2f%n", recompensa);
                } 
                else {
                    System.out.println("fail: comando invalido");
                }
            }   
        }
}
```


## Sugestões para Próximas Questões Reais

1. **Open/Closed Principle (OCP) em Geração de Relatórios:**
    
    - **Contexto:** Um sistema de alunos precisa gerar relatórios em diferentes formatos (CSV, HTML, PDF).
        
    - **Foco:** Forçar o uso de uma interface `GeradorDeRelatorio` para que um novo formato (ex: JSON) possa ser adicionado sem modificar a classe principal `SistemaDeAlunos`.
        
2. **Interface Segregation Principle (ISP) em Funcionários de Logística:**
    
    - **Contexto:** Uma interface `Trabalhador` com métodos como `dirigirCaminhao()`, `gerenciarEstoque()`, `atenderTelefone()`.
        
    - **Foco:** Mostrar que um `Estagiário` não precisa implementar `dirigirCaminhao()`. A interface deve ser quebrada em `IDirigivel`, `IGerenciavel`, `IAtendivel`.
        
3. **Dependency Inversion Principle (DIP) em Notificações:**
    
    - **Contexto:** Um `ProcessadorDePedido` envia uma notificação de conclusão usando uma classe concreta `EmailService`.
        
    - **Foco:** Introduzir a interface `INotificador`. Fazer o `ProcessadorDePedido` depender de `INotificador` para que ele possa usar `SmsService` ou `PushService` sem mudanças.