
#Concluded 

---

- **Extração de Método**:  Solução para "Métodos Longos" e "Código Duplicado". Consiste em pegar um trecho de código dentro de um método longo e movê-lo para um novo método (geralmente privado) com um nome claro e autoexplicativo.
    
- **Extração de Classe** Mencionado como a solução para "Classes Grandes" e "Código Duplicado". Consiste em pegar um conjunto de atributos e métodos relacionados de uma classe grande e movê-los para uma nova classe menor e mais coesa. A classe original passa a ter uma referência para a nova classe.
    
- **Inline Method** O oposto da Extração de Método. É usado quando o corpo de um método é muito pequeno. A operação remove o método e insere seu corpo diretamente nos locais onde ele era chamado.
    
- **Movimentação de Método** Move um método de uma classe A para uma classe B. Isso é feito quando o método usa mais serviços, atributos ou métodos da classe B do que da sua própria classe A, melhorando a coesão . É a solução para o _code smell_ "Feature Envy".
    
- **Pull Up Method**: Um tipo de movimentação de método onde um método presente em duas ou mais subclasses é movido para a superclasse comum, eliminando a duplicação .
    
- **Push Down Method**: Um método que está na superclasse, mas só é usado por uma algumas subclasses, é movido para as subclasses onde ele realmente faz sentido .
- 
- **Renomeação:** Um dos refatorings mais simples e importantes. Dar nomes claros a variáveis, métodos e classes é fundamental para a legibilidade.    
    

    
- **Remoção de Código :** Deleta métodos, classes, variáveis ou atributos que não são mais usados ou chamados por nenhuma parte do sistema .


    

    

    

    

    
- **Renomeação (Rename)** Um dos refactorings mais comuns e importantes. Consiste em dar um nome mais adequado, claro e significativo a um elemento de código (como variável, método, classe ou parâmetro) e atualizar todas as referências a ele .
    
- **Extração de Variáveis (Extract Variable)** Usado para simplificar expressões complexas. A operação quebra a expressão em partes menores, armazenando os resultados parciais em variáveis temporárias com nomes claros, tornando o código mais fácil de ler .
    
- **Remoção de Flags** Simplifica a lógica de laços ao remover variáveis de controle (_flags_) e substituí-las por comandos de fluxo de controle mais diretos, como `break` ou `return` .
    
- **Substituição de Condicional por Polimorfismo** Refatora um comando `switch` ou `if/else` complexo que verifica o tipo de um objeto. A lógica de cada ramo da condicional é movida para um método específico em cada subclasse, e a chamada condicional é substituída por uma única chamada de método polimórfico .
    
- **Remoção de Código Morto (Remove Dead Code)** Consiste em deletar código que não é mais usado por nenhuma parte do sistema, como métodos que nunca são chamados, classes que nunca são instanciadas, ou atributos e variáveis que nunca são lidos .