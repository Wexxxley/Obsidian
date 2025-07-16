

---
#### **Semana 2: Aberto/Fechado (O) e Substituição de Liskov (L)**

- **Meta da Semana:** Aprender a estender o comportamento do software sem modificar o código existente.
    
- **Segunda-feira:**
    
    - **Teoria:** Estude o **Princípio Aberto/Fechado (OCP)**. Entenda como o uso de interfaces e classes abstratas permite adicionar novas funcionalidades sem alterar classes que já foram testadas.
        
    - **Prática:** No seu "kata" da semana anterior, adicione uma nova regra de desconto (ex: "Desconto para cliente VIP"). Faça isso sem alterar a classe de cálculo original, aplicando o OCP.
        
- **Quarta-feira:**
    
    - **Teoria:** Mergulhe no **Princípio da Substituição de Liskov (LSP)**. O foco é entender a importância de uma hierarquia de herança consistente.
        
    - **Prática:** Crie um exemplo clássico que quebra o LSP (como a famosa relação Quadrado/Retângulo) e depois corrija. O objetivo é sentir na prática o problema que o LSP resolve.
        
- **Sexta-feira:**
    
    - **Teoria:** Revise OCP e LSP juntos. Eles estão muito conectados. Entenda como o LSP garante que o OCP funcione corretamente.
        
    - **Prática:** Continue seu projeto pessoal ou o "kata", aplicando os três princípios vistos até agora (S, O, L). Tente identificar pontos onde você pode usar herança de forma segura.
        

---

#### **Semana 3: Segregação de Interfaces (I) e Inversão de Dependência (D)**

- **Meta da Semana:** Dominar o desacoplamento, a chave para um software flexível e testável.
    
- **Segunda-feira:**
    
    - **Teoria:** Estude o **Princípio da Segregação de Interfaces (ISP)**. O conceito é simples: "Interfaces específicas são melhores que interfaces genéricas".
        
    - **Prática:** Imagine uma interface "Trabalhador" com os métodos `trabalhar()` e `receberSalario()`. Agora, crie classes `FuncionarioCLT` e `Robo`. Note que `Robo` não deveria ter o método `receberSalario()`. Refatore isso usando o ISP, criando interfaces menores.
        
- **Quarta-feira:**
    
    - **Teoria:** Foco no **Princípio da Inversão de Dependência (DIP)**. Este é o mais transformador! Entenda a frase: "Dependa de abstrações, não de implementações".
        
    - **Prática:** No seu projeto, encontre um lugar onde uma classe de alto nível cria uma instância de uma classe de baixo nível (ex: `new RepositorioDeUsuario()`). Refatore para que a classe de alto nível receba a dependência (a abstração/interface) pelo construtor.
        
- **Sexta-feira:**
    
    - **Revisão Geral do S.O.L.I.D.:** Junte tudo! Faça um mapa mental ou um resumo com suas próprias palavras sobre cada um dos cinco princípios.
        
    - **Prática:** Faça uma revisão completa no seu projeto/kata. Identifique e anote violações de cada um dos 5 princípios. Escolha uma para corrigir.
        

---

#### **Semana 4: Object Calisthenics e Prática Integradora**

- **Meta da Semana:** Aplicar regras práticas para "limpar" o código e consolidar todo o conhecimento adquirido.
    
- **Segunda-feira:**
    
    - **Teoria:** Estude as 9 regras do **Object Calisthenics**. Não precisa decorar, mas entenda o objetivo por trás de cada uma. Foque nestas 4 para começar:
        
        1. Um nível de indentação por método.
            
        2. Não use a palavra-chave `else`.
            
        3. Encapsule todos os tipos primitivos.
            
        4. Um ponto por linha (Lei de Demeter).
            
    - **Prática:** Pegue um método do seu projeto que tenha um `if/else` aninhado e refatore-o para usar polimorfismo ou _early returns_, eliminando o `else`.
        
- **Quarta-feira:**
    
    - **Teoria:** Aprofunde-se na regra "Encapsule todos os tipos primitivos". Entenda o conceito de "Objetos de Valor".
        
    - **Prática:** No seu projeto, substitua um `String` ou `int` por uma classe de valor. Por exemplo, troque `String email` por uma classe `Email` que se autovalida no construtor. Troque `double preco` por uma classe `Dinheiro`.
        
- **Sexta-feira:**
    
    - **Desafio Final:** Comece um novo "kata" do zero. Desta vez, seu objetivo principal não é apenas fazer funcionar, mas aplicar ativamente todos os princípios do S.O.L.I.D. e as regras do Object Calisthenics que você aprendeu.
        
    - **Autoavaliação:** Compare o código deste novo kata com o do projeto que você analisou na primeira semana. Veja a diferença. Sinta o progresso!
        

**Dica de Ouro:** Não tenha pressa. É melhor passar duas semanas em um único princípio até entendê-lo de verdade do que passar por todos superficialmente. A maestria vem da repetição e da prática deliberada.

Bom estudo!