
#Concluded 

---
## **Histórias de Usuário**

A técnica dos 3 c's  ajuda a montar as históras
1. **Cartão:** Cartão físico (ou digital) onde o cliente escreve, em poucas sentenças uma funcionalidade que ele deseja. 
2. **Conversas:** Os detalhes são preenchidos através de conversas entre os clientes e os desenvolvedores. 
3. **Confirmação:** São os critérios de aceitação da história, definidos pelo cliente.

Recomenda-se listar os papéis dos principais usuários do sistema, para evitar que os requisitos atendam apenas a um grupo específico. As histórias costumam seguir o formato: "Como um **papel de usuário**, eu gostaria de realizar **algo com o sistema**".

**Exemplos para "Usuário Típico"**
• Como usuário típico, eu gostaria de **realizar empréstimos de livros**.
• Como usuário típico, eu gostaria de **devolver um livro** que tomei emprestado.
• Como usuário típico, eu gostaria de **renovar empréstimos** de livros.

**Exemplos para "Professor":**
• Como professor, eu gostaria de realizar **empréstimos de maior duração**.
• Como professor, eu gostaria de **sugerir a compra de livros**.
• Como professor, eu gostaria de **doar livros para a biblioteca**.

**Exemplos para "Funcionário da Biblioteca"**
• Como funcionário da biblioteca, eu gostaria de **cadastrar novos usuários**.
• Como funcionário da biblioteca, eu gostaria de **cadastrar novos livros**.
• Como funcionário da biblioteca, eu gostaria de **dar baixa em livros estragados**

---
### **Como especificar requisitos não-funcionais usando histórias?**
    
-  É um desafio, pois requisitos não-funcionais (como desempenho, segurança, etc.) geralmente se aplicam a todo o sistema ou a várias funcionalidades, e não se encaixam bem no formato de uma história que é entregue em uma única iteração 1.
        
    - Uma história como "o tempo de resposta deve ser de 1 segundo" não faz sentido ser alocada a uma iteração específica, pois é uma preocupação constante2.
        
    - A melhor abordagem é: o dono do produto pode escrever histórias sobre requisitos não-funcionais, mas elas são usadas principalmente para **reforçar os critérios de conclusão** (Definition of Done - DoD) das histórias funcionais3.
        
    - Por exemplo, para uma história funcional ser considerada "concluída", ela pode precisar passar por uma revisão de código focada em desempenho, ou testes específicos de desempenho podem ser realizados antes de uma _release_ 4.
        
    - Em resumo, essas histórias sobre requisitos não-funcionais geralmente não entram no _backlog_ do produto da mesma forma que as funcionais, mas servem para refinar o que significa "pronto" 5.
        
2. **É possível criar histórias para estudo de uma nova tecnologia?**
    
    - Conceitualmente, **não**. Histórias devem sempre ser escritas e priorizadas pelos clientes e devem entregar valor para o negócio 6. Uma história como "estudar o framework X" viola esse princípio7.
        
    - No entanto, o estudo de uma nova tecnologia pode ser uma **tarefa** necessária para implementar uma história de usuário funcional8.
        
    - Tarefas que têm como objetivo a aquisição de conhecimento ou a redução de risco técnico são chamadas de **spikes**9.
        

Essas são as perguntas frequentes abordadas sobre histórias de usuários. Digite "next" para passarmos aos Casos de Uso.