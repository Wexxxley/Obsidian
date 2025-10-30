
#Concluded 

---

Refactoring é um <mark style="background: #ADCCFFA6;">conjunto de transformações no código que melhoram sua estrutura interna (manutenibilidade), mas sem alterar seu comportamento externo (funcionamento).</mark>

- **O objetivo é:** Melhorar a legibilidade, modularidade, testabilidade e facilita o entendimento e futuras modificações.
### **Por que Refatorar? (Leis de Lehman)**

1. Um sistema de software <mark style="background: #ADCCFFA6;">deve ser continuamente mantido para se adaptar ao seu ambiente. </mark>Esse processo deve continuar até o ponto em que se torna mais vantajoso substituí-lo por um sistema completamente novo.
2. À medida que um sistema sofre manutenções, <mark style="background: #ADCCFFA6;">sua complexidade interna aumenta e a qualidade de sua estrutura deteriora-se, a não ser que um trabalho seja realizado</mark> para estabilizar ou evitar tal fenômeno

---
### **Quando Refatorar? (Oportunista vs. Planejado)**

- A forma mais comum e recomendada é o **Refactoring Oportunista**:
    - É feito em pequenos passos, o tempo todo, misturado com as tarefas normais de desenvolvimento .
    - Ao corrigir um bug ou adicionar uma nova funcionalidade, você percebe um trecho de código ruim e o melhora _imediatamente_ para facilitar seu trabalho atual .
    
- O **Planejado** é usado para modificações mais profundas, demoradas e complexas. Por ser complexo, esse tipo de refatoração é realizado em **sessões planejadas e dedicadas**.

---
