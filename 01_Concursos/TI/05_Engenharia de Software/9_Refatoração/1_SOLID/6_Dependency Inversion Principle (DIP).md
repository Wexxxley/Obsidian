
> [!NOTE]
> Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender de abstrações

Esse princípio diz que uma classe não deve depender de implementações de outras classes, mas sim de abstrações/interfaces/contratos. Com isso temos como benefício o desacoplamento, pois é fácil trocar implementações sem impactar o código. Outra vantagem é a facilidade para testar, uma vez que podemos simular um cenário sem depender da implementação real. 

Por exemplo, vamos supor que nosso sistema dependa de um repositório. Esse repositório pode ser um real ou uma interface. A vantagem da interface é que a implementação e o database utilizado não importa.

No exemplo, PedidoService não depende da implementação de um repositório, mas sim de uma interface.

```java

public interface IPedidoRepository {
    void salvarPedido(String pedido);
}

// Implementação concreta do repositório
public class PedidoRepository implements IPedidoRepository {
    @Override
    public void salvarPedido(String pedido) {
        System.out.println("Pedido salvo no banco de dados.");
    }
}

// Camada de serviço que depende da abstração (não da implementação)
public class PedidoService {
    private final IPedidoRepository repository;

    // Injeção de dependência via construtor
    public PedidoService(IPedidoRepository repository) {
        this.repository = repository;
    }

    public void processarPedido(String pedido) {
        repository.salvarPedido(pedido);
    }
}

```
  
  
  