

---
“As entidades de software (classes, módulos, funções) devem ser abertas para ampliação, mas fechadas para modificação”.  

Quando uma única mudança resulta em uma sucessão de mudanças nos módulos dependentes, o projeto tem um grande problema. O OCP nos aconselha a refatorar o sistema para que alterações não causem mais modificações. Se o OCP for bem aplicado, **mudanças são obtidas pela adição de novo código e não pela alteração de código antigo que já funciona.**

Os módulos que obedecem ao OCP têm duas características principais:
1. **São abertos para ampliação**: À medida que os requisitos do aplicativo mudam, podemos ampliar o módulo com novos comportamentos que satisfaçam essas alterações. 
2. **São fechados para modificação**: Ampliar o comportamento de um módulo não resulta em mudanças no código-fonte. 
  
 **Como é possível modificar os comportamentos de um módulo sem alterar seu código-fonte?**  A resposta é: com **abstração**. Em qualquer  linguagem de programação orientada a objetos, é possível criar abstrações fixas e que ainda assim representam um grupo ilimitado de comportamentos possíveis. As abstrações são classes base abstratas e o grupo ilimitado de comportamentos possíveis é representado por todas as classes derivadas possíveis.

  

 Um módulo pode manipular uma abstração. Tal módulo pode ser fechado para modificação, pois ele depende de uma abstração fixa. Apesar disso, o comportamento desse módulo pode ser ampliado pela criação de novas derivadas da abstração.**