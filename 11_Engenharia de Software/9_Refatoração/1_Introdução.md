

---

Refactoring é um <mark style="background: #ADCCFFA6;">conjunto de transformações no código que melhoram sua estrutura interna (manutenibilidade), mas sem alterar seu comportamento externo (funcionamento).</mark>

- **O objetivo é:** Melhorar a legibilidade, modularidade, testabilidade e facilita o entendimento e futuras modificações.
### **Por que Refatorar? (Leis de Lehman)**

1. Um sistema de software <mark style="background: #ADCCFFA6;">deve ser continuamente mantido para se adaptar ao seu ambiente. </mark>Esse processo deve continuar até o ponto em que se torna mais vantajoso substituí-lo por um sistema completamente novo.
2. À medida que um sistema sofre manutenções, <mark style="background: #ADCCFFA6;">sua complexidade interna aumenta e a qualidade de sua estrutura deteriora-se, a não ser que um trabalho seja realizado</mark> para estabilizar ou evitar tal fenômeno

### **Quando Refatorar? (Oportunista vs. Planejado)**

- Refactoring não deve ser uma fase separada, longa e planejada ("vamos parar tudo por 2 meses para refatorar").
    
- A forma mais comum e recomendada é o **Refactoring Oportunista**:
    
    - É feito em pequenos passos, o tempo todo, misturado com as tarefas normais de desenvolvimento .
        
    - Ao corrigir um bug ou adicionar uma nova funcionalidade, você percebe um trecho de código ruim e o melhora _imediatamente_ para facilitar seu trabalho atual .
        

**4. O Pré-requisito MAIS IMPORTANTE: Testes**

- A prática de refactoring depende **criticamente** da existência de uma boa suíte de testes automatizados (especialmente testes de unidade).
    
- **Refatorar sem testes é extremamente arriscado** .
    
- Os testes são a "rede de segurança" que garante que a transformação no código não alterou o comportamento externo do sistema . Se você refatorar e os testes continuarem passando, você tem alta confiança de que não quebrou nada.
    

**5. O que Procurar? (Code Smells)**

- _Code Smells_ (ou "maus cheiros" no código) são os **indicadores** de que um trecho de código pode precisar de refatoração . Eles não são erros, mas sinais de problemas estruturais.
    
- Os dois _smells_ mais importantes citados são:
    
    1. **Código Duplicado:** É o principal _smell_. Aumenta o esforço de manutenção (uma mudança precisa ser feita em vários lugares) e o risco de bugs (esquecer de atualizar uma das cópias) .
        
    2. **Métodos Longos:** Métodos devem ser pequenos. Métodos longos são difíceis de entender, manter e reutilizar .
        

**6. Exemplos Chave de Operações de Refactoring**

- **Extração de Método:** É o refactoring mais comum. Pega-se um trecho de código dentro de um método longo e o move para um novo método (privado) com um nome claro. Isso combate o _smell_ de Métodos Longos.
    
- **Movimentação de Método:** Move um método de uma classe A para uma classe B, geralmente porque o método usa mais recursos da classe B (combatendo o _smell_ de _Feature Envy_) . Melhora a coesão.
    
- **Renomeação:** Um dos refatorings mais simples e importantes. Dar nomes claros a variáveis, métodos e classes é fundamental para a legibilidade .