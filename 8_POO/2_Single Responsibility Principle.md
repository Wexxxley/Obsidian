
---

> **A class should have one, and only one, reason to change.**

Sabemos que os **requisitos mudam com o tempo**. Cada uma dessas mudanças altera a responsabilidade de, no mínimo, uma classe. Quanto mais responsabilidades sua classe possui, mais frequentemente você precisa alterá-la. 

Além disso, afeta todos os componentes que dependem da classe alterada. Dependendo da alteração, você pode precisar atualizar as dependências ou recompilar as classes dependentes, ainda que elas não sejam diretamente afetadas pela sua mudança. Elas usam apenas uma das outras responsabilidades implementadas por sua classe, mas você precisa atualizá-las mesmo assim.

No fim das contas, você precisa alterar sua classe com mais frequência, e cada alteração é mais complicada, tem mais efeitos colaterais e requer muito mais trabalho do que deveria. Portanto, é melhor evitar esses problemas garantindo que cada classe tenha apenas uma responsabilidade. Além disso, se você quiser entender melhor o que está acontecendo em sua aplicação, pode usar a solução de perfilamento de código da Retrace


### **Mais Fácil de Entender**
Classes, componentes de software e microsserviços que têm apenas uma responsabilidade são muito mais fáceis de explicar, entender e implementar do que aqueles que oferecem uma solução para tudo. 

No entanto, tome cuidado para não simplificar demais o seu código. Alguns desenvolvedores **levam o princípio da responsabilidade única ao extremo**, criando classes com apenas um método. Mais tarde, ao escreverem o código de fato, eles precisam injetar muitas dependências, tornando o código confuso. Portanto, o princípio da responsabilidade única é uma regra importante para tornar seu código mais compreensível, mas não o use como uma verdade absoluta. Use o bom senso ao desenvolver.

### **Uma Pergunta Simples para Validar Seu Design**

O princípio da responsabilidade única parece muito mais fácil do que costuma ser.

Se você constrói seu software por um longo período e precisa adaptá-lo a requisitos que mudam, pode parecer que a abordagem mais fácil e rápida é adicionar um método ou funcionalidade ao seu código existente em vez de escrever uma nova classe ou componente. Mas isso  resulta em classes com mais de uma responsabilidade e torna a manutenção do software cada vez mais difícil.

Você pode evitar esses problemas fazendo uma pergunta simples antes de realizar qualquer alteração: **Qual é a responsabilidade da sua classe/componente?**

Se sua resposta inclui a palavra **“e”**, você está quebrando o princípio da responsabilidade única. Para dar um exemplo mais concreto, vamos supor que temos uma classe para um funcionário que contém métodos para **calcular e armazenar** seu salário.  Se seguirmos o princípio da responsabilidade única, essas classes deveriam ser divididas, pois as funções de negócio são bem diferentes.

 Se uma classe tem mais de uma responsabilidade, as responsabilidades se tornam acopladas. Mudanças em uma responsabilidade podem prejudicar a capacidade da classe de cumprir as outras. Outra forma de entender SRP é: uma classe tem que se preocupar em responder somente a um grupo de atores.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeAoCKuGPHogBt1apdpuTXAwh2qLXLp6LihsRS3I3zjo7r4e5v-PcR8RHFNFDXZLJv-8Julf-DVHadYVVuXS-5Nwv0xoNX17Adi9twtzvosUAa4oVNV5HMzj2B95kt4msGU9YY3fQ?key=VJjD-GQ4BeMLFSL3weHQfxOz)

 No exemplo, a classe Rectangle tem dois métodos. Um desenha o retângulo na tela e o outro calcula a área do retângulo. Dois atores diferentes usam a classe, um  deles o usa para ajudar na matemática geométrica e nunca desenha o retângulo.  O outro ator é gráfico, mas pode efetuar geometria.

  

 Esse projeto viola o SRP pois a Rectangle tem duas responsabilidades: fornecer um modelo matemático de um retângulo e representar o retângulo em uma GUI. A violação do SRP causa vários problemas. Um deles é: se for necessário alterar o cálculo de área para se adequar a GraphicalApplication, essa mudança poderá afetar o outro ator que utiliza o método area.

 Um projeto melhor é separar as duas responsabilidades em duas classes. Assim cada classe responderia a somente um grupo de atores.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc2HCr2hxDkzAB1Ddhm-5HHmsIo8D94ksJ08P4Uj3RvM8qu7UAkwHvWn9bq3JRwGD22Wpal_3khLj5a4qUhjg5lfj-rWRqgtRvWQC_LCOuWueoqgkU9nPktFHhtwxxX4tqOMoMl?key=VJjD-GQ4BeMLFSL3weHQfxOz)

  

Definindo responsabilidade: No contexto do SRP, definimos uma responsabilidade como um motivo para mudar. Se você consegue pensar em mais de um motivo para mudar uma classe, essa classe tem mais de uma responsabilidade. 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfY2nblZzX-fYC0vAAwPmxoVgsFci1E6fhnbtqfqJAIAOKjW1RdB0MntHvSgaOq1wmn8udnvz4oKRxqr_UQeo5kRWNzfq4VAwrog5Vud31Qx0FFlv20fgRd17Z_80mpuJ4NLut7?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Note que Boleto cria uma implementação de enviar Email, mas e se a lógica de enviar email  mudar?

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfSv2LXaBDjDKZ_dI67WyjOaIPaCBmCIrp4lR3MH7naxNqQnnrfxaCwO607b_FB1KMcZ-5v45KNAED-mWtp6qqpoi1UA98nWTPylGzHtgvMrMqM5YS5FW5ZAqqHM9y8AOqqiCoh2A?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Agora, boleto depende de uma classe email para gerar emails.

**