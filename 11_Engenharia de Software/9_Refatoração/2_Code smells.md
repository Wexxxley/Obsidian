

---
Code Smells são os **indicadores** de que um trecho de código pode precisar de refatoração . 
    
- **Código Duplicado:** Ocorre quando o mesmo trecho de código aparece em vários lugares, o que aumenta o esforço de manutenção e o risco de bugs.
    
- **Métodos Longos:** Métodos devem ser pequenos. 
    
- **Classes Grandes:** Classes que assumem muitas responsabilidades ou não são coesas.
    
- **Feature Envy (Inveja de Funcionalidade):** Ocorre quando um método de uma classe A parece "invejar" outra classe B, ou seja, ele acessa mais dados e métodos da classe B do que da sua própria classe A . A solução geralmente é mover o método para a classe B.
    
- **Métodos com Muitos Parâmetros:** Métodos devem ter poucos parâmetros para serem fáceis de entender e usar .
    
- **Variáveis Globais:** Devem ser evitadas, pois criam um acoplamento ruim entre as partes do sistema. 
    
- **Obsessão por Tipos Primitivos:** Ocorre quando tipos primitivos são usados no lugar de classes pequenas para representar conceitos (ex: usar `String` para um CEP) .
    
- **Objetos Mutáveis:** Objetos cujo estado pode ser modificado após a criação. O livro considera isso um _smell_, pois objetos imutáveis (que não podem ser alterados) são mais simples e seguros de usar, especialmente em programação concorrente .
    
- **Classes de Dados:** Classes que possuem apenas atributos, mas nenhuma lógica. 
    
- **Comentários:** Comentários podem ser um _smell_ quando são usados para explicar um código ruim. A recomendação é: "Não comente código ruim, reescreva-o" . 