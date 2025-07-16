

---
Object Calisthenics é um conjunto de 9 regras de programação. O objetivo não é seguir essas regras cegamente como leis, mas usá-las como um guia para praticar e desenvolver hábitos que levam a um código orientado a objetos de melhor qualidade.

1. **Use apenas um nível de indentação por método**
    - **Por quê?** Força a extração de lógica complexa para novos métodos menores e com nomes claros. Isso resulta em funções focadas e mais fáceis de ler.

2. **Não use a palavra-chave `else`**
    
    - **O que significa:** Evite completamente o uso de `else`.
        
    - **Por quê?** Incentiva o uso de padrões como _early returns_ (retornos antecipados ou _guard clauses_), polimorfismo ou objetos de estratégia. O código resultante geralmente é mais linear e direto ao ponto.
        
3. **Encapsule todos os tipos primitivos (e Strings)**
    
    - **O que significa:** Não passe tipos primitivos (como `int`, `String`, `double`) soltos pelo sistema. Envolva-os em classes.
        
    - **Por quê?** Promove a criação de **Value Objects** (Objetos de Valor). Em vez de um `String email`, crie uma classe `Email` que se autovalida. Isso concentra o comportamento e as regras de validação junto com o dado, evitando lógica duplicada.
        
4. **Use coleções de primeira classe**
    
    - **O que significa:** Qualquer classe que contém uma coleção não deve ter nenhum outro membro.
        
    - **Por quê?** Força a criação de classes específicas para gerenciar coleções (ex: uma classe `ListaDePedidos` em vez de um `List<Pedido>`). Isso cria um local natural para colocar métodos de negócio relacionados àquela coleção (ex: `pedidos.calcularTotal()`, `pedidos.encontrarPedidosCancelados()`).
        
5. **Um ponto por linha**
    
    - **O que significa:** Evite encadear chamadas de métodos, como `pedido.getCliente().getEndereco().getCidade()`.
        
    - **Por quê?** É uma aplicação da **Lei de Demeter**. Longas cadeias de chamadas criam um forte acoplamento entre as classes. Se a classe `Cliente` mudar a forma como armazena o `Endereco`, seu código quebra. Em vez disso, a classe `Pedido` deveria ter um método como `pedido.obterCidadeDoCliente()`.
        
6. **Não abrevie**
    
    - **O que significa:** Use nomes completos e explícitos para classes, métodos e variáveis. `CalculadorDeImpostoSobreVenda` em vez de `CalcImpVnd`.
        
    - **Por quê?** O código é lido muito mais vezes do que é escrito. Nomes claros tornam o código auto documentado e dramaticamente mais fácil de entender.
        
7. **Mantenha todas as entidades pequenas**
    
    - **O que significa:** Imponha limites artificiais, como não mais que 50 linhas por classe e 10 classes por pacote.
        
    - **Por quê?** É uma regra de choque para forçá-lo a pensar sobre a **coesão** e a **responsabilidade única**. Se uma classe está ficando grande, provavelmente ela está fazendo coisas demais e precisa ser dividida.
        
8. **Nenhuma classe com mais de duas variáveis de instância**
    
    - **O que significa:** Uma classe não deve ter mais de dois atributos (variáveis de instância).
        
    - **Por quê?** Esta é uma das regras mais difíceis e controversas. Ela força você a questionar se a sua classe tem uma única responsabilidade coesa. Frequentemente, quando uma classe tem muitos atributos, alguns deles podem ser agrupados em um novo objeto, resultando em um design mais coeso.
        
9. **Nenhum Getter/Setter/Propriedade**
    
    - **O que significa:** Evite expor o estado interno de um objeto através de métodos `get` e `set`.
        
    - **Por quê?** Esta regra promove o princípio **"Tell, Don't Ask"** (Mande, Não Pergunte). Em vez de pegar dados de um objeto para tomar uma decisão fora dele, você deve mandar uma mensagem para o objeto e deixá-lo tomar a decisão internamente com seus próprios dados. Isso é encapsulamento de verdade.
        

---

### Por que usar?

O objetivo principal do Object Calisthenics é servir como uma ferramenta de aprendizado e reflexão. Ao tentar aplicar essas regras, você é forçado a pensar de forma diferente sobre seu design, o que naturalmente te empurra para soluções mais robustas, desacopladas e verdadeiramente orientadas a objetos.