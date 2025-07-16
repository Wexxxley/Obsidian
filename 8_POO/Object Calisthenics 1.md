
#Concluded 

---
Object Calisthenics é um conjunto de 9 regras de programação. O objetivo não é seguir essas regras cegamente como leis, mas usá-las como um guia para praticar e desenvolver hábitos que levam a um código orientado a objetos de melhor qualidade.

1. **Use apenas um nível de indentação por método**
    - **Por quê?** Força a extração de lógica complexa para novos métodos menores e com nomes claros. Isso resulta em funções focadas e mais fáceis de ler.

2. **Evite a palavra-chave `else`**
    - **Por quê?** Incentiva o uso de padrões como **_early returns_** (retornos antecipados), polimorfismo ou objetos de estratégia. O código resultante geralmente é mais linear e direto ao ponto.
	![400](../../attachments/Pasted%20image%2020250716080720.png)
	![450](../../attachments/Pasted%20image%2020250716080822.png)
	
3. **Encapsule todos os tipos primitivos**
    - Não passe tipos primitivos (como `int`, `String`, `double`) soltos. Envolva-os em classes.
    - **Por quê?** Promove a criação de **Value Objects**. Por exemplo, em vez de um `String email`, crie uma classe `Email` que se autovalida. Isso concentra o comportamento e regras de validação junto com o dado.
	![550](../../attachments/Pasted%20image%2020250716082649.png)
