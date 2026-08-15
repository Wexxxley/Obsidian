
#Concluded 

---
Code Smells são **indicadores** de que um trecho de código pode precisar de refatoração. Note que os code smells estão ligado aos principios SOLID.  
    
1. **Código Duplicado:** Ocorre quando o mesmo trecho de código aparece em vários lugares.
    
2. **Métodos Longos:** Métodos devem ser pequenos. 
    
3. **Classes Grandes:** Classes que assumem muitas responsabilidades ou não são coesas.
    
4. **Feature Envy (Inveja de Funcionalidade):** Ocorre quando um método de uma classe A parece "invejar" outra classe B, ou seja, ele acessa mais dados e métodos da classe B do que da sua própria classe A  A solução geralmente é mover o método para a classe B.
    ![300](../../../../attachments/Pasted%20image%2020260815134000.png) ![300](../../../../attachments/Pasted%20image%2020260815134025.png)
5. **Métodos com Muitos Parâmetros:** Métodos devem ter poucos parâmetros para serem fáceis de entender e usar.
    
6. **Variáveis Globais:** Variáveis globais devem ser evitadas porque quebra o princípio do encapsulamento. Essa exposição gera **alto acoplamento**. Adicionalmente, o estado global inviabiliza a execução isolada de testes e introduz riscos críticos de concorrência.
    
7. **Obsessão por Tipos Primitivos:** Ocorre quando tipos primitivos são usados no lugar de classes pequenas para representar conceitos (ex: usar `String` para um CEP) .
    
- **Objetos Mutáveis:** Objetos cujo estado pode ser modificado após a criação. A crítica não é sobre a existência da mutabilidade em si, mas sobre o **uso desnecessário** dela
	    
	1. A recomendação é "minimizar o número de tais objetos, sem, no entanto, imaginar que vamos eliminá-los por completo".
	2. A crítica é direcionada principalmente a **objetos que representam valores simples**. O livro sugere que classes como `CEP`, `Moeda`, `Endereco`, `Data`, `Hora`, `Fone` e `Email` deveriam, preferencialmente, ser imutáveis.
	    
- **Classes de Dados:** Classes que possuem apenas atributos, mas nenhuma lógica. 
    
- **Comentários:** Comentários podem ser um smell quando são usados para explicar um código ruim. A recomendação é: "Não comente código ruim, reescreva-o" . 