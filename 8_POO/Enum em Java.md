
#Concluded 

---

Enum é um tipo de dado especial que serve para representar um conjunto fixo de constantes nomeadas.

Pense em coisas que têm um número limitado e predefinido de valores:
- Dias da semana (SEGUNDA, TERÇA, QUARTA...)
- Meses do ano (JANEIRO, FEVEREIRO, MARÇO...)
- Status de um pedido (PROCESSANDO, ENVIADO, ENTREGUE, CANCELADO)
- Operações bancárias (DEPOSITO, COBRANÇA, SAQUE, ...)

---
### Por que usar Enum? 

Antes dos enums, usavam constantes de String ou int para representar esses valores. Isso gerava vários problemas:
    - **Sem segurança:** Você pode passar qualquer String ou int, não apenas os valores válidos.
    - **Propenso a erros:** Erros de digitação não são pegos pelo compilador.

O Enum soluciona tudo isso, além de melhorar a legibilidade.

---
### Sintaxe Básica

A declaração mais simples.
![](attachments/Pasted%20image%2020250809120536.png)

Um `enum` não é apenas uma lista de nomes, ele é uma **classe especial**. Um enum pode ter:
- **Atributos**    
- **Construtores (PRIVATE)** 
- **Métodos**

Cada constante que você declara no enum é, na verdade, um objeto `public static final`, uma instância única da classe do enum.

#### Exemplo Avançado

```
// O enum é uma classe chamada TipoOperacao
public enum TipoOperacao {

    // Cada um deles é um objeto public static final que chama o construtor
    DEPOSITO("Depósito em Conta"),
    TARIFA("Cobrança de Tarifa Mensal"),
    SAQUE("Saque no Caixa Eletrônico"),
    ESTORNO("Estorno de Compra");

    // 1. Atributo (campo) de instância
    private final String descricao;

    // 2. Construtor (obrigatoriamente private)
    // É chamado uma vez para cada constante do enum na inicialização.
    TipoOperacao(String descricao) {
        this.descricao = descricao;
    }

    // 3. Método de instância
    public String getDescricao() {
        return this.descricao;
    }
}
```

**Como usar o enum inteligente:**

Java

```
TipoOperacao op = TipoOperacao.TARIFA;

System.out.println("Tipo da Operação: " + op); // Imprime TARIFA
System.out.println("Descrição: " + op.getDescricao()); // Imprime "Cobrança de Tarifa Mensal"
```

---

### Métodos Úteis Embutidos

Todo enum em Java já vem com alguns métodos estáticos úteis:

- **`values()`**: Retorna um array com todas as constantes do enum. Ótimo para iterações.
    
    Java
    
    ```
    for (TipoOperacao tipo : TipoOperacao.values()) {
        System.out.println(tipo + " -> " + tipo.getDescricao());
    }
    ```
    
- **`valueOf(String nome)`**: Converte uma `String` de volta para uma instância do enum.
    
    Java
    
    ```
    // Converte a string "DEPOSITO" para o objeto TipoOperacao.DEPOSITO
    TipoOperacao tipo = TipoOperacao.valueOf("DEPOSITO");
    ```
    
- **`name()`**: Retorna o nome da constante como uma `String` (ex: `"DEPOSITO"`).
    
- **`ordinal()`**: Retorna a posição (baseada em zero) da constante na declaração do enum. **Cuidado:** É perigoso usar `ordinal()` em lógica de negócio, pois se a ordem das constantes mudar, sua lógica quebra.
    

### Resumo das Vantagens

1. **Segurança de Tipo (Type Safety):** Garante que apenas valores válidos sejam usados.
    
2. **Legibilidade:** O código fica muito mais claro e fácil de entender (`StatusPedido.ENTREGUE` é melhor que `2`).
    
3. **Poder e Flexibilidade:** A capacidade de adicionar atributos e métodos transforma suas constantes em objetos ricos e poderosos.
    
4. **Agrupamento Lógico:** Mantém um conjunto de constantes relacionadas bem organizadas em um único lugar.