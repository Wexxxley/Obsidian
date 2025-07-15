
---

> **A class should have one, and only one, reason to change.**

**Porque usar isso?**
The argument for the single responsibility principle is simple: it makes your software easier to implement and prevents unexpected side effects of future changes.

Sabemos que os requisitos mudam com o tempo. Cada uma dessas mudanças altera a responsabilidade de, no mínimo, uma classe. Quanto mais responsabilidades sua classe possui, mais frequentemente você precisa alterá-la. Se sua classe implementa múltiplas responsabilidades, elas deixam de ser independentes umas das outras.

Você precisa alterar sua classe assim que uma de suas responsabilidades muda. Isso é, obviamente, mais frequente do que seria necessário se ela tivesse apenas uma responsabilidade.

Isso pode não parecer um grande problema, mas também afeta todas as classes ou componentes que dependem da classe alterada. Dependendo da alteração, você pode precisar atualizar as dependências ou recompilar as classes dependentes, ainda que elas não sejam diretamente afetadas pela sua mudança. Elas usam apenas uma das outras responsabilidades implementadas por sua classe, mas você precisa atualizá-las mesmo assim.

No fim das contas, você precisa alterar sua classe com mais frequência, e cada alteração é mais complicada, tem mais efeitos colaterais e requer muito mais trabalho do que deveria. Portanto, é melhor evitar esses problemas garantindo que cada classe tenha apenas uma responsabilidade. Além disso, se você quiser entender melhor o que está acontecendo em sua aplicação, pode usar a solução de perfilamento de código da Retrace