

---
4. **Use coleções de primeira classe**
    - Qualquer classe que contém uma coleção não deve ter nenhum outro membro.
    - **Por quê?** Força a criação de classes específicas para gerenciar coleções (ex: uma classe `ListaDePedidos` em vez de um `List<Pedido>`). Isso cria um local natural para colocar métodos de negócio relacionados àquela coleção (ex: `pedidos.calcularTotal()`, `pedidos.encontrarPedidosCancelados()`).
    
5. **Um ponto por linha**
    - Evite encadear chamadas de métodos, como `pedido.getCliente().getEndereco().getCidade()`.
    - **Por quê?** Longas cadeias de chamadas criam um forte acoplamento entre as classes. Se a classe `Cliente` mudar a forma como armazena o `Endereco`, seu código quebra. Em vez disso, a classe `Pedido` deveria ter um método como `pedido.obterCidadeDoCliente()`.
        
6. **Não abrevie**
    - Use nomes explícitos para classes, métodos e variáveis. `CalculadorDeImpostoSobreVenda` em vez de `CalcImpVnd`.
    - **Por quê?** O código é lido muito mais vezes do que é escrito. Nomes claros tornam o código auto documentado mais fácil de entender.
        
7. **Mantenha todas as entidades pequenas**
    - Imponha limites artificiais, como não mais que 50 linhas por classe.
    - **Por quê?** É uma regra de choque para forçá-lo a pensar sobre a **coesão** e a **responsabilidade única**. Se uma classe está ficando muito grande, provavelmente ela está fazendo coisas demais e precisa ser dividida.
        
8. **Nenhuma classe com mais de duas variáveis de instância**
    - Uma classe não deve ter mais de dois atributos (variáveis de instância).
    - **Por quê?** Esta é uma das regras mais difíceis e controversas. Ela força você a questionar se a sua classe tem uma única responsabilidade coesa. Frequentemente, quando uma classe tem muitos atributos, alguns deles podem ser agrupados em um novo objeto, resultando em um design mais coeso.
        
9. **Evite Getters e Setters**
    - Evite expor o estado interno de um objeto através de métodos `get` e `set`.
    - **Por quê?** Esta regra promove o princípio **"Tell, Don't Ask"** (Mande, Não Pergunte). Em vez de pegar dados de um objeto para tomar uma decisão fora dele, você deve mandar uma mensagem para o objeto e deixá-lo tomar a decisão internamente com seus próprios dados. Isso é encapsulamento de verdade.
    