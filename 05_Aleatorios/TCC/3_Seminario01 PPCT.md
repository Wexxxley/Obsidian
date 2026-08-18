

---

### The effectiveness of test-driven development approach on software projects: A multi-case study.
A eficácia da abordagem de desenvolvimento orientado a testes em projetos de software: um estudo de múltiplos casos.

**CONCEITOS ABORDADOS** 

- **Complexidade ciclomática:** basicamente,  conta-se quantas decisões lógicas (como if, for e operadores lógicos) existem em uma função, indicando o quão difícil ela é de testar e manter. 

- **Complexidade essencial:** Sua finalidade é medir o grau de construções não estruturadas presentes (o que n são if e for, como goto, return, break, continue) em um  módulo.

- **Complexidade de Design do Módulo:** quando um módulo principal (uma função) precisa invocar outros submódulos (funções subordinadas) para concluir sua tarefa. Essa métrica ajuda a identificar quais módulos atuam como controladores complexos do sistema, pois será necessário criar testes de integração.

**CONTEXTO DO TRABALHO**

**Problemática**: uma vez que exige a estruturação de testes para funcionalidades que ainda não foram codificadas e trás uma ideia de queda de produtividade inicialmente.


![](../../attachments/Pasted%20image%2020260814171422.png)

**Figura 5 e Tabela 6: Avaliação de Complexidade**
- **Complexidade Essencial (ev(G)):** O TDD registrou 1.48, contra 5.10 do NON-TDD, indicando um código com estruturas lógicas mais simples e diretas.
- **Complexidade de Design (iv(G)):** O TDD obteve 1.58, em contraste com 7.45 do NON-TDD, refletindo uma arquitetura de módulos e chamadas muito menos intrincada.
- **Complexidade Ciclomática (v(G)):** O TDD marcou apenas 2.0, enquanto o NON-TDD chegou a 7.45, evidenciando que a abordagem sem testes gerou um código com excesso de ramificações condicionais.



    

### Metodologia de Medição e Cálculo

- A obtenção destas métricas ocorre através da aplicação de procedimentos voltados para a análise estrutural da decisão dos módulos.
    

    




![](../../attachments/Pasted%20image%2020260814172356.png)    
- **Cobertura de Testes (Test coverage):** A equipe TDD atingiu 86% de cobertura, contra apenas 61% da equipe não-TDD.

- **Defeitos Pré-Lançamento (Pre-release defect):** A equipe TDD identificou e registrou 16 falhas antes da entrega do software, um número drasticamente menor que as 42 falhas encontradas pela equipe não-TDD durante a mesma fase.

- **Defeitos Pós-Lançamento (Post-release defect):** Após o software entrar em ambiente de produção (uso real), apenas 10 erros foram reportados na versão TDD, em contraste com 27 erros relatados na versão não-TDD. 
