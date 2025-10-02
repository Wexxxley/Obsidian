A principal motivação para o **Object Calisthenics** é aplicar alguns princípios do **SOLID.** Basicamente são um conjunto de **boas práticas** para aumentar a qualidade do seu código. O objetivo não é seguir essas regras cegamente como leis, mas usá-las como um guia para praticar e desenvolver hábitos que levam a um código orientado a objetos de melhor qualidade.

1. **Use apenas um nível de indentação por método**
    - **Por quê?** Força a extração de lógica complexa para novos métodos menores e com nomes claros. Isso resulta em funções focadas e mais fáceis de ler.

2. **Evite a palavra-chave `else`**
    - **Por quê?** Incentiva o uso de padrões como **retornos antecipados**. O código resultante geralmente é mais linear e direto ao ponto.

	![400](../../attachments/Pasted%20image%2020250716080720.png)

	![450](../../attachments/Pasted%20image%2020250716080822.png)

3. **Encapsule todos os tipos primitivos** ==EASY==
    - Ecite passar tipos primitivos (como `int`, `String`, `double`) soltos. Envolva-os em classes.
    - **Por quê?** Promove a criação de **Value Objects**. Por exemplo, em vez de um `String email`, crie uma classe `Email` que se autovalida. 

	![550](../../attachments/Pasted%20image%2020250716082649.png)

4. **Use coleções de primeira classe**
    - Qualquer classe que contém uma coleção não deve ter nenhum outro membro.
    - **Por quê?** Força a criação de classes específicas para gerenciar coleções (ex: uma classe `ListaDePedidos`). Isso cria um local natural para colocar métodos de negócio relacionados àquela coleção.

5. **Um ponto por linha**
    - Evite encadear chamadas de métodos, como `pedido.getCliente().getEndereco().getCidade()`.
    - **Por quê?** Longas cadeias de chamadas criam um forte acoplamento entre as classes. Se a classe `Cliente` mudar a forma como armazena o `Endereco`, seu código quebra. Em vez disso, a classe `Pedido` deveria ter um método como `pedido.obterCidadeDoCliente()`.

6. **Não abrevie** ==EASY==
    - Use nomes explícitos para classes, métodos e variáveis. `CalculadorDeImpostoSobreVenda.
    - **Por quê?** O código é lido muito mais vezes do que é escrito. Nomes claros tornam o código auto documentado mais fácil de entender.

7. **Mantenha todas as entidades pequenas** ==EASY==
    - Imponha limites artificiais, como não mais que 50 linhas por classe.
    - **Por quê?** É uma regra de choque para forçá-lo a pensar sobre a **coesão** e a **responsabilidade única**. Se uma classe está ficando muito grande, provavelmente ela está fazendo coisas demais e precisa ser dividida.

8. **Nenhuma classe com mais de duas variáveis de instância** 
    - Uma classe não deve ter mais de dois atributos (variáveis de instância).
    - **Por quê?** Esta é uma das regras mais difíceis e controversas. Ela força você a questionar se a sua classe tem uma única responsabilidade coesa. Frequentemente, quando uma classe tem muitos atributos, alguns deles podem ser agrupados em um novo objeto.

9. **Evite Getters e Setters** ==EASY==
    - Evite expor o estado interno de um objeto através de métodos `get` e `set`.
    - **Por quê?** Esta regra promove o princípio **Tell, Don't Ask** (Mande, Não Pergunte). Em vez de você pegar dados de um objeto para tomar uma decisão fora dele, você deve mandar uma mensagem para o objeto (através de métodos) e deixá-lo tomar a decisão internamente com seus próprios dados. Isso é encapsulamento.
    