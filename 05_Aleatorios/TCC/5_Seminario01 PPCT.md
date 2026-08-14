

---

### The effectiveness of test-driven development approach on software projects: A multi-case study.

- A eficácia da abordagem de desenvolvimento orientado a testes em projetos de software: um estudo de múltiplos casos.

![](../../attachments/Pasted%20image%2020260814171422.png)
**Figura 4: Produtividade e Satisfação**
- **Satisfação:** A equipe que utilizou a abordagem TDD alcançou um nível de satisfação 
    
      
    
- **Produtividade:** As barras indicam que a produtividade bruta entre as duas equipes é praticamente idêntica, havendo apenas uma margem mínima de vantagem para o método TDD.
    
      
    

### Figura 5 e Tabela 6: Avaliação de Complexidade

Esta seção mensura o nível de complexidade estrutural do código. Em métricas de complexidade, valores menores indicam um código mais limpo e fácil de manter.

  

- **Complexidade Essencial (ev(G)):** O TDD registrou 1.48, contra 5.10 do NON-TDD, indicando um código com estruturas lógicas muito mais simples e diretas.
    
      
    
- **Complexidade de Design (iv(G)):** O TDD obteve 1.58, em contraste com os alarmantes 7.45 do NON-TDD, refletindo uma arquitetura de módulos e chamadas muito menos intrincada.
    
      
    
- **Complexidade Ciclomática (v(G)):** O TDD marcou apenas 2.0, enquanto o NON-TDD chegou a 7.45, evidenciando que a abordagem sem testes gerou um código com excesso de caminhos de execução independentes (ramificações condicionais), o que dificulta a manutenção e os testes futuros.
    
      
    

### Figura 6 e Tabela 7: Avaliação de Design (Métricas MOOD)

Esta seção avalia a qualidade da orientação a objetos implementada pelas equipes.

  

- **Fator de Ocultação de Atributo (AHF):** O TDD (85.11%) superou drasticamente o NON-TDD (45.79%), demonstrando que o uso de testes guiou a equipe a construir classes com um nível de encapsulamento de dados muito superior.
    
      
    
- **Fator de Herança de Atributo (AIF):** A equipe NON-TDD (83.22%) utilizou ligeiramente mais herança de dados do que a equipe TDD (78.41%).
    
      
    
- **Fator de Acoplamento (CF):** Este é o indicador mais crítico do gráfico. O TDD manteve o acoplamento em 23.62%, enquanto o NON-TDD atingiu 75.44%. Um acoplamento baixo é essencial na Engenharia de Software, pois prova que o sistema TDD possui dependências mínimas entre as classes, sendo altamente modular.
    
      
    
- **Fator de Ocultação de Método (MHF / MHS no gráfico):** A equipe NON-TDD (19.56%) ocultou um volume um pouco maior de métodos operacionais do que a equipe TDD (12.33%).
    
      
    
- **Fator de Polimorfismo (PF):** A abordagem TDD alcançou 108%, indicando um uso ligeiramente superior de sobrescrita e interfaces polimórficas em comparação ao NON-TDD (95%).