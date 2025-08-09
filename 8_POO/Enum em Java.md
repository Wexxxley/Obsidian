
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
### Sintaxe

A declaração mais simples de um enum é uma lista de constantes:

Java

```
public enum StatusPedido {
    PROCESSANDO,
    ENVIADO,
    ENTREGUE,
    CANCELADO; // O ponto e vírgula é opcional aqui, mas necessário se houver mais código.
}
```

**Como usar:** Você pode declarar variáveis desse tipo e usá-las de forma segura, especialmente em estruturas como o `switch`.

Java

```
// Declarando e atribuindo
StatusPedido meuPedido = StatusPedido.ENVIADO;

// Usando em um switch (muito comum e seguro)
switch (meuPedido) {
    case PROCESSANDO:
        System.out.println("Seu pedido está sendo preparado.");
        break;
    case ENVIADO:
        System.out.println("Seu pedido já foi enviado!");
        break;
    case ENTREGUE:
        System.out.println("Pedido entregue com sucesso.");
        break;
    case CANCELADO:
        System.out.println("Este pedido foi cancelado.");
        break;
    default:
        System.out.println("Status desconhecido.");
        break;
}
```

O compilador garante que você só pode usar os valores definidos no `Enum`. Tentar usar `StatusPedido.PAGO` (que não existe) daria um erro de compilação.

---

### Enums são Classes Especiais (O Grande Poder do Java)

É aqui que o Java brilha. Um `enum` não é apenas uma lista de nomes, ele é compilado como uma **classe especial**. Isso significa que um enum pode ter:

- **Atributos (campos)**
    
- **Construtores** (que são sempre `private`)
    
- **Métodos**
    

Cada constante que você declara no enum (como `PROCESSANDO`) é, na verdade, um objeto `public static final`, uma instância única da classe do enum.

#### Exemplo Avançado: O Enum "Inteligente"

Vamos usar o `TipoOperacao` que vimos antes. Ele é um exemplo perfeito de um enum "inteligente".

Java

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