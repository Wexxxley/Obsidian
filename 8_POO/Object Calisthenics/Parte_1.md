A principal motivação para o **Object Calisthenics** é aplicar alguns princípios do **SOLID.** Basicamente são um conjunto de **boas práticas** para aumentar a qualidade do seu código. O objetivo não é seguir essas regras cegamente como leis, mas usá-las como um guia para praticar e desenvolver hábitos que levam a um código orientado a objetos de melhor qualidade.

#### **1. Use apenas um nível de indentação por método**
- **Por quê?** Força a extração de lógica complexa para novos métodos menores e com nomes claros. Isso resulta em funções focadas e mais fáceis de ler.
#### **2. Evite a palavra-chave `else`**
 - **Por quê?** Incentiva o uso de padrões como **retornos antecipados**. O código resultante geralmente é mais linear e direto ao ponto.

##### **Exemplos abrangendo regras 1 e 2:**

Código antes
```java
public boolean podeAcessarAntes(Usuario usuario) {
    if (usuario != null) {
        if (usuario.getIdade() >= 18) {
            if (usuario.isAtivo()) {
                return true;
            } else {
                // else aninhado
                System.out.println("Erro: Usuário inativo.");
                return false;
            }
        } else {
            // else aninhado
            System.out.println("Erro: Usuário menor de idade.");
            return false;
        }
    } else {
        // else principal
        System.out.println("Erro: Usuário não encontrado.");
        return false;
    }
}
```

Código refatorado
```java
public boolean podeAcessarDepois(Usuario usuario) {
    if (usuario == null) {
        System.out.println("Erro: Usuário não encontrado.");
        return false;
    }

    if (usuario.getIdade() < 18) {
        System.out.println("Erro: Usuário menor de idade.");
        return false;
    }

    if (!usuario.isAtivo()) {
        System.out.println("Erro: Usuário inativo.");
        return false;
    }

    // Se passou por todas as verificações, o acesso é permitido.
    return true;
}
```

---
#### **3. Encapsule tipos primitivos**
- Evite passar tipos primitivos (como `int`, `String`, `double`) soltos. Envolva-os em classes.
    - **Por quê?** Promove a criação de **Value Objects**. Por exemplo, em vez de um `String email`, crie uma classe `Email` que se autovalida. 

```java
public final class Email {
    private final String valor; 

    public Email(String valor) {
        // A validação acontece DENTRO do construtor.
        if (valor == null || !isFormatoValido(valor)) {
            throw new IllegalArgumentException("Formato inválido.");
        }
        this.valor = valor;
    }

    // Método de validação privado e centralizado.
    private boolean isFormatoValido(String email) {
        // Validação simples apenas para o exemplo.
        return email.contains("@") && email.contains(".");
    }
}
```

---
#### **4. Use coleções de primeira classe**
- Qualquer classe que contém uma coleção não deve ter nenhum outro membro.
- **Por quê?** Força a criação de classes específicas para gerenciar coleções (ex: uma classe `ListaDePedidos`). Isso cria um local natural para colocar métodos de negócio relacionados àquela coleção.

```java
public class RepositorioPedidos {
    private Map<Integer, Pedido> pedidos;

    public RepositorioPedidos() {
        this.pedidos = new HashMap<>();
    }

    public void salvarPedido(Pedido pedido) {
        pedidos.put(pedido.getId(), pedido);
    }

    public Pedido buscarPedido(int id) {
        return pedidos.get(id);
    }
}
```

---
#### **5. Um ponto por linha**
 - Evite encadear chamadas de métodos, como `pedido.getCliente().getEndereco().getCidade()`.
    - **Por quê?** Longas cadeias de chamadas criam um forte acoplamento entre as classes. Se a classe `Cliente` mudar a forma como armazena o `Endereco`, seu código quebra. Em vez disso, a classe `Pedido` deveria ter um método como `pedido.obterCidadeDoCliente()`.

```java
public static void demonstrarAntes() {
    Cidade cidade = new Cidade("São Paulo");
    Endereco endereco = new Endereco(cidade);
    Cliente cliente = new Cliente(endereco);
    PedidoAntes pedido = new PedidoAntes(cliente);

    // Se qualquer uma dessas relações mudar, este código quebra!
    String nomeDaCidade = pedido.getCliente().getEndereco().getCidade().getNome();
}
```

```java
public static void demonstrarDepois() {
    Cidade cidade = new Cidade("São Paulo");
    Endereco endereco = new Endereco(cidade);
    Cliente cliente = new Cliente(endereco);
    PedidoDepois pedido = new PedidoDepois(cliente);

    // O código cliente apenas pede ao 'pedido' a informação que deseja.
    String nomeDaCidade = pedido.obterNomeDaCidadeDoCliente();
}
```

---
####  **6. Não abrevie**
- Use nomes explícitos para classes, métodos e variáveis. `CalculadorDeImpostoSobreVenda.
    - **Por quê?** O código é lido muito mais vezes do que é escrito. Nomes claros tornam o código auto documentado mais fácil de entender.
####  **7. Mantenha todas as entidades pequenas**
- Imponha limites artificiais, como não mais que 50 linhas por classe.
- **Por quê?** É uma regra de choque para forçá-lo a pensar sobre a **coesão** e a **responsabilidade única**. Se uma classe está ficando MUITO grande, provavelmente ela está fazendo coisas demais e precisa ser dividida.
#### **8. Nenhuma classe com mais de duas variáveis de instância** 
 - Uma classe não deve ter mais de dois atributos (variáveis de instância).
-  **Por quê?** Esta é uma das regras mais controversas. Ela força você a questionar se a sua classe tem uma única responsabilidade coesa. Frequentemente, quando uma classe tem muitos atributos, alguns deles podem ser agrupados em um novo objeto.
#### **9. Evite Getters e Setters** 
- Evite expor o estado interno de um objeto através de métodos `get` e `set`.
- **Por quê?** Esta regra promove o princípio **Tell, Don't Ask** (Mande, Não Pergunte). Em vez de você pegar dados de um objeto para tomar uma decisão fora dele, você deve mandar uma mensagem para o objeto (através de métodos) e deixá-lo tomar a decisão internamente com seus próprios dados. Isso é encapsulamento.

```java
// MÁ PRÁTICA - Apenas um "recipiente de dados"
public class ContaBancaria {
    private double saldo;

    public ContaBancaria(double saldoInicial) {
        this.saldo = saldoInicial;
    }

    // Getter expõe o estado interno
    public double getSaldo() {
        return saldo;
    }

    // Setter permite que qualquer um modifique o estado
    public void setSaldo(double novoSaldo) {
        this.saldo = novoSaldo;
    }
}

// ------ Classe que USA a ContaBancaria (Ex: um caixa eletrônico) ------
public class CaixaEletronico {
    public void executarSaque(ContaBancaria conta, double valor) {
        // 1. PERGUNTA pelo estado do objeto
        double saldoAtual = conta.getSaldo();
        // 2. TOMA A DECISÃO FORA do objeto
        if (saldoAtual >= valor) {
            double novoSaldo = saldoAtual - valor;
            // 3. MODIFICA o estado do objeto por fora
            conta.setSaldo(novoSaldo)
            
            System.out.println("Saque realizado com sucesso. Novo saldo: R$" + conta.getSaldo());
        } else {
            System.out.println("Falha na operação: Saldo insuficiente.");
        }
    }
}
```


```java
// BOA PRÁTICA - Objeto com comportamento e estado protegidos
public class ContaBancaria {
    private double saldo;

    public ContaBancaria(double saldoInicial) {
        this.saldo = saldoInicial;
    }
    
    // Comportamento para adicionar dinheiro
    public void depositar(double valor) {
        if (valor > 0) {
            this.saldo += valor;
            System.out.println("Depósito de R$" + valor + " realizado. Novo saldo: R$" + this.saldo);
        }
    }

    // Comportamento para retirar dinheiro. A própria classe decide!
    public boolean sacar(double valor) {
        if (valor > 0 && this.saldo >= valor) {
            this.saldo -= valor;
            return true; // Informa que a operação foi um sucesso
        }
        return false; // Informa que a operação falhou
    }

    // Não temos mais getSaldo() ou setSaldo() públicos. 
    // Se precisarmos exibir o saldo, podemos ter um método específico.
    public void exibirSaldo() {
        System.out.println("O saldo atual é: R$" + this.saldo);
    }
}

// ------ Classe que USA a ContaBancaria (Ex: um caixa eletrônico) ------
public class CaixaEletronico {
    public void executarSaque(ContaBancaria conta, double valor) {
        System.out.println("Tentando sacar R$" + valor);

        // 1. MANDA uma ordem para o objeto
        // O objeto toma a decisão internamente
        boolean sucesso = conta.sacar(valor);

        // 2. Reage ao resultado da operação
        if (sucesso) {
            System.out.println("Saque realizado com sucesso.");
            conta.exibirSaldo();
        } else {
            System.out.println("Falha na operação: Saldo insuficiente ou valor inválido.");
        }
    }
}
```