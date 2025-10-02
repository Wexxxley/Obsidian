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