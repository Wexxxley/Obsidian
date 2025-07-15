
---

> **A class should have one, and only one, reason to change.**

Sabemos que os requisitos mudam com o tempo. Cada uma dessas mudanças altera a responsabilidade de, no mínimo, uma classe. Quanto mais responsabilidades sua classe possui, mais frequentemente você precisa alterá-la. 

Isso pode não parecer um grande problema, mas também afeta todos os componentes que dependem da classe alterada. Dependendo da alteração, você pode precisar atualizar as dependências ou recompilar as classes dependentes, ainda que elas não sejam diretamente afetadas pela sua mudança. Elas usam apenas uma das outras responsabilidades implementadas por sua classe, mas você precisa atualizá-las mesmo assim.

No fim das contas, você precisa alterar sua classe com mais frequência, e cada alteração é mais complicada, tem mais efeitos colaterais e requer muito mais trabalho do que deveria. Portanto, é melhor evitar esses problemas garantindo que cada classe tenha apenas uma responsabilidade. Além disso, se você quiser entender melhor o que está acontecendo em sua aplicação, pode usar a solução de perfilamento de código da Retrace


### **Mais Fácil de Entender**
Classes, componentes de software e microsserviços que têm apenas uma responsabilidade são muito mais fáceis de explicar, entender e implementar do que aqueles que oferecem uma solução para tudo. 

No entanto, tome cuidado para não simplificar demais o seu código. Alguns desenvolvedores **levam o princípio da responsabilidade única ao extremo**, criando classes com apenas um método. Mais tarde, ao escreverem o código de fato, eles precisam injetar muitas dependências, tornando o código confuso. Portanto, o princípio da responsabilidade única é uma regra importante para tornar seu código mais compreensível, mas não o use como uma verdade absoluta. Use o bom senso ao desenvolver.

### **Uma Pergunta Simples para Validar Seu Design**

O princípio da responsabilidade única parece muito mais fácil do que costuma ser.

Se você constrói seu software por um longo período e precisa adaptá-lo a requisitos que mudam, pode parecer que a abordagem mais fácil e rápida é adicionar um método ou funcionalidade ao seu código existente em vez de escrever uma nova classe ou componente. Mas isso  resulta em classes com mais de uma responsabilidade e torna a manutenção do software cada vez mais difícil.

Você pode evitar esses problemas fazendo uma pergunta simples antes de realizar qualquer alteração: **Qual é a responsabilidade da sua classe/componente?**

Se sua resposta inclui a palavra **“e”**, você muito provavelmente está quebrando o princípio da responsabilidade única. Nesse caso, é melhor dar um passo para trás e repensar sua abordagem atual. Muito provavelmente, existe uma maneira melhor de implementá-la.

Para dar um exemplo mais concreto, vamos supor que temos uma classe para um funcionário que contém métodos para **calcular e reportar** seu salário. Em outras palavras, o cálculo do salário pode ser classificado como ler dados e manipulá-los posteriormente.

Enquanto isso, reportar o salário é uma operação de persistência de dados, onde os dados são armazenados em algum meio de armazenamento. Se seguirmos o princípio da responsabilidade única de Martin, essas classes deveriam ser divididas, pois as funções de negócio são bem diferentes.

A seguir, vamos ver alguns exemplos do mundo real em Java sobre o princípio da responsabilidade única.