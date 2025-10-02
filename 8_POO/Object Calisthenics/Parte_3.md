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

public class CaixaEletronico {
    public void executarSaque(ContaBancaria conta, double valor) {
        // 1. PERGUNTA pelo estado do objeto
        double saldoAtual = conta.getSaldo();
        // 2. TOMA A DECISÃO FORA do objeto
        if (saldoAtual >= valor) {
            double novoSaldo = saldoAtual - valor;
            // 3. MODIFICA o estado do objeto por fora
            conta.setSaldo(novoSaldo)
        }
    }
}
```

Refatorado
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
        }
    }
    // Comportamento para retirar dinheiro. A própria classe decide!
    public boolean sacar(double valor) {
        if (valor > 0 && this.saldo >= valor) {
            this.saldo -= valor;
            return true; 
        }
        return false
    }
    // Se precisarmos exibir o saldo, podemos ter um método específico.
    public void exibirSaldo() {
        System.out.println("O saldo atual é: R$" + this.saldo);
    }
}

public class CaixaEletronico {
    public void executarSaque(ContaBancaria conta, double valor) {
        // 1. MANDA uma ordem para o objeto
        boolean sucesso = conta.sacar(valor);
        // 2. Reage ao resultado da operação
        if (sucesso) {
            System.out.println("Saque realizado com sucesso.");
        } else {
            System.out.println("Falha na operação.");
        }
    }
}
```

**LEMBRANDO QUE**:  O objetivo não é seguir essas regras cegamente como leis, mas usá-las como um guia para praticar e desenvolver hábitos que levam a um código de melhor qualidade.