
#Concluded 

---
### **1 Heterogeneidade**

Os sistemas distribuídos devem ser construídos a partir de uma variedade de redes, hardware de computador, sistemas operacionais e linguagens de programação diferentes.

1. **Redes:** Diferentes tipos de redes (Ethernet, Wi-Fi, etc.) são unificadas pelos **Protocolos Internet**
2. **Hardware e SO:** Computadores têm diferentes arquiteturas e sistemas operacionais.
3. **Linguagens de Programação:** Diferentes linguagens usam diferentes representações para dados e estruturas.
4. **Desenvolvimento:** Programas só se comunicam se seguirem **padrões comuns** (protocolos e representação de dados).

#### **2.1.1 Middleware**
O **Middleware** ==é a principal solução para mascarar a heterogeneidade==. É uma camada de software que fornece uma **abstração de programação uniforme**, escondendo as diferenças de rede, hardware, SO e linguagens subjacentes.
#### **2.1.2 Migração de Código (Máquina Virtual)**
A **Migração de Código** visa resolver o problema de um programa executável ser amarrado a uma **arquitetura de hardware** e a um **Sistema Operacional**. A **Máquina Virtual** é a solução para tornar o código portátil.

1. **Código Intermediário:** O compilador da linguagem (ex: Java, C#) não gera código de máquina nativo. Em vez disso, ele gera um **código intermediário**.
2. **VM como tradutor:** A Máquina Virtual (como o **CLR** do .NET) é um programa que atua como um **tradutor**. Ela é a única parte do sistema que é específica ao hardware e ao SO.
3. **Execução em Qualquer Lugar:** Para rodar o código, basta que o computador tenha a VM instalada. A VM recebe o código intermediário, entende o que ele precisa fazer e o **traduz** para o sistema específico.

---
### **2.2 Segurança**

A segurança em sistemas distribuídos é crucial devido ao alto valor dos recursos compartilhados e tem três componentes principais: **Confidencialidade** (proteção contra acesso não autorizado), **Integridade** (proteção contra alteração ou dano) e **Disponibilidade** (garantir acesso aos recursos).

1. **Comunicação Segura:** O principal desafio é enviar **informações sigilosas** pela rede. Isso exige **criptografia** para ocultar o conteúdo da mensagem.
2. **Identificação Confiável:** É fundamental **saber a identidade** do agente remoto. 
3. **Ataque de Negação de Serviço:** Um invasor **interrompe a disponibilidade** do serviço bombardeando-o com requisições sem sentido, impedindo que usuários legítimos o utilizem.

---
### **2.3 Escalabilidade**

A **escalabilidade** é a capacidade de um sistema distribuído permanecer eficiente diante de um aumento significativo no **número de usuários e recursos**.

Os principais desafios no projeto de sistemas escaláveis são:
1. **Controlar o Custo dos Recursos Físicos:** O custo para suportar n usuários deve se **proporcional** ao numero de máquinas. Se um servidor suporta 20 usuários, dois devem suportar 40. Isso exige a adição eficiente de servidores para evitar gargalos.
2. **Controlar a Perda de Desempenho:** O tempo de acesso aos dados não deve aumentar linearmente. Algoritmos devem usar **estruturas hierárquicas** (ex: DNS), onde a perda de desempenho é minimizada para **O(logn)**.
3. **Impedir o Esgotamento de Recursos de Software:** Deve-se prever a demanda futura para evitar que recursos de software críticos se esgotem.
4. **Evitar Gargalos de Desempenho:** Algoritmos e gerenciamento de dados devem ser **descentralizados**. O **DNS** resolveu o gargalo do sistema predecessor, que usava um único arquivo central, ao **particionar a tabela de nomes** entre diversos servidores distribuídos.

==Técnicas essenciais para melhorar a escalabilidade incluem a **replicação de dados** e o uso de **cache** para recursos muito acessados.==

---
### **2.4 Tratamento de Falhas**

As falhas em um sistema distribuído são parciais – isto é, alguns componentes falham, enquanto outros continuam funcionando. Portanto, o tratamento de falhas é particularmente difícil. 

**Detecção de falhas:** algumas falhas podem ser detectadas. Por exemplo, somas de verificação podem ser usadas para detectar dados corrompidos. O desafio é gerenciar a ocorrência de falhas que não podem ser detectadas.

**Mascaramento de falhas:** algumas falhas detectadas podem ser ocultas ou se tornar menos sérias. 
1. Mensagens podem ser retransmitidas quando não chegam. 
2. Dados podem ser gravados em dois discos, para que, se um estiver danificado, o outro ainda possa estar correto. 

**Tolerância a falhas**: a maioria dos serviços na Internet apresenta falhas. Seus clientes podem ser projetados de forma a tolerar falhas. Por exemplo, quando um navegador não consegue contatar um servidor Web, ele não faz o usuário esperar indefinidamente, ele informa o usuário sobre o problema, deixando-o livre para tentar novamente. 

**Redundância**: os serviços podem se tornar tolerantes a falhas com o uso de componentes redundantes. 
1. Sempre deve haver pelo menos duas rotas entre dois roteadores quaisquer na Internet. 
2. No Domain Name System, toda tabela de correspondência de nomes é replicada em pelo menos dois servidores diferentes. 
3. Um banco de dados pode ser replicado em vários servidores, para garantir que os dados permaneçam acessíveis após a falha de qualquer servidor.

---
### **2.5 Concorrência** 

Tanto os serviços como os aplicativos fornecem recursos que podem ser compartilhados pelos clientes em um sistema distribuído. Portanto, existe a possibilidade de que vários clientes tentem acessar um recurso compartilhado ao mesmo tempo. O processo que gerencia um recurso compartilhado poderia aceitar e tratar um pedido de cliente por vez. Contudo, essa estratégia limita o desempenho. Portanto, os serviços permitem que vários pedidos de cliente sejam processados concorrentemente. Para tornar isso mais concreto, suponha que cada recurso seja encapsulado como um objeto e que as ==chamadas sejam executadas em diferentes fluxos de execução, processos ou threads, concorrentes==. 

Portanto, o objeto que gerencia o recurso compartilhado é responsável por garantir a **coerência** em um ambiente concorrente. Para isso, o programador deve ==**sincronizar** as operações internas do objeto usando técnicas padrão, como **semáforos**==, garantindo que os dados permaneçam consistentes, apesar do acesso simultâneo.

