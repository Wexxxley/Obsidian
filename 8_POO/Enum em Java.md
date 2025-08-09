
#Concluded 

---

Enum é um tipo de dado especial que serve para representar um conjunto fixo de constantes nomeadas.

Pense em coisas que têm um número limitado e predefinido de valores:
- Dias da semana (SEGUNDA, TERÇA, QUARTA...)
- Meses do ano (JANEIRO, FEVEREIRO, MARÇO...)
- Status de um pedido (PROCESSANDO, ENVIADO, ENTREGUE, CANCELADO)
- Operações bancárias (DEPOSITO, COBRANÇA, SAQUE, ...)

---
### **Por que usar Enum?** 
Antes dos enums, usavam constantes de String ou int para representar esses valores. Isso gerava vários problemas:
    - **Sem segurança:** Você pode passar qualquer String ou int, não apenas os valores válidos.
    - **Propenso a erros:** Erros de digitação não são pegos pelo compilador.

O Enum soluciona tudo isso, além de melhorar a legibilidade.

---
### **Sintaxe Básica**
A declaração mais simples.
![](attachments/Pasted%20image%2020250809120536.png)

Um `enum` não é apenas uma lista de nomes, ele é uma **classe especial**. Um enum pode ter:
- **Atributos**    
- **Construtores (PRIVATE)** 
- **Métodos**

Cada constante que você declara no enum é, na verdade, um objeto `public static final`, uma instância única da classe do enum.

---
### **Métodos Úteis** 
Todo enum em Java já vem com alguns métodos estáticos úteis:

- **values()**: Retorna um array com todas as constantes do enum.
- **valueOf(String nome)**: Converte uma String para uma instância do enum.
- **name()**: Retorna o nome da constante como uma String.
- **ordinal()**: Retorna a posição da constante na declaração do enum. 

---
### **Uso avançado**

![](attachments/Pasted%20image%2020250809122914.png)