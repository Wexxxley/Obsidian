
---

> **A class should have one, and only one, reason to change.**
### **1 Porque usar SRP?**
Sabemos que os **requisitos mudam com o tempo**. Cada uma dessas mudanças altera a responsabilidade de, no mínimo, uma classe. Quanto mais responsabilidades sua classe possui, mais frequentemente você precisa alterá-la. 

No fim das contas, você precisa alterar sua classe com mais frequência, e cada alteração é mais complicada, tem mais efeitos colaterais e requer muito mais trabalho do que deveria. Classes e componentes que têm apenas uma responsabilidade são muito mais fáceis de explicar, entender e implementar do que aqueles que oferecem uma solução para tudo. 

No entanto, tome cuidado para não simplificar demais o seu código. Alguns desenvolvedores **levam o princípio da responsabilidade única ao extremo**, criando classes com apenas um método. O princípio da responsabilidade única é uma regra importante para tornar seu código mais compreensível, mas não o use como uma verdade absoluta. Use o bom senso ao desenvolver.

---
### **2. Pergunta Simples para Validar Seu Design**

Faça a seguinte pergunta: **Qual é a responsabilidade da sua classe/componente?** ou
**Quais os motivos para mudar a minha classe tem?**

Se sua resposta inclui a palavra **“e”**, você está quebrando o princípio da responsabilidade única. 
![250](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfY2nblZzX-fYC0vAAwPmxoVgsFci1E6fhnbtqfqJAIAOKjW1RdB0MntHvSgaOq1wmn8udnvz4oKRxqr_UQeo5kRWNzfq4VAwrog5Vud31Qx0FFlv20fgRd17Z_80mpuJ4NLut7?key=VJjD-GQ4BeMLFSL3weHQfxOz)
Note que Boleto cria uma implementação de enviar Email, mas e se a lógica de enviar email  mudar?

![250](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfSv2LXaBDjDKZ_dI67WyjOaIPaCBmCIrp4lR3MH7naxNqQnnrfxaCwO607b_FB1KMcZ-5v45KNAED-mWtp6qqpoi1UA98nWTPylGzHtgvMrMqM5YS5FW5ZAqqHM9y8AOqqiCoh2A?key=VJjD-GQ4BeMLFSL3weHQfxOz)
Agora, boleto depende de uma classe email para gerar emails. Boleto não precisa mais se preocupar em como gerar email, essa responsabilidade ficou a serviço de outra classe.


Se uma classe tem mais de uma responsabilidade, as responsabilidades se tornam acopladas. Mudanças em uma responsabilidade podem prejudicar a capacidade da classe de cumprir as outras. Outra forma de entender SRP é: uma classe tem que se preocupar em responder somente a um grupo de atores.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeAoCKuGPHogBt1apdpuTXAwh2qLXLp6LihsRS3I3zjo7r4e5v-PcR8RHFNFDXZLJv-8Julf-DVHadYVVuXS-5Nwv0xoNX17Adi9twtzvosUAa4oVNV5HMzj2B95kt4msGU9YY3fQ?key=VJjD-GQ4BeMLFSL3weHQfxOz)
