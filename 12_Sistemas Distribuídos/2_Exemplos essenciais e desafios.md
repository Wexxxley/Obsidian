
___

## **1. Exemplos**
### **1.1 Massively multiplayer online games (MMOGs)**

A engenharia dos MMOGs representa um grande desafio para as tecnologias de sistemas distribuídos, devido à necessidade de tempos de resposta rápidos para preservar a experiência dos usuários do jogo. Outros desafios incluem a propagação de eventos em tempo real para muitos jogadores e a manutenção de uma visão coerente do mundo compartilhado. Foram propostas várias soluções para o projeto de MMOGs:

- O jogo online, o EVE Online, utiliza uma **arquitetura cliente-servidor** na qual uma **única cópia do estado do mundo é mantida em um servidor centralizado e acessada por programas clientes em execução nos consoles dos jogadores**. O servidor é uma entidade complexa, consistindo em um cluster caracterizada por centenas de nós de computador. A arquitetura centralizada ajuda significativamente no gerenciamento do mundo virtual e a cópia única também diminui as preocupações com a coerência. Assim, o objetivo é garantir resposta rápida, para isso a carga é particionada por meio da alocação de sistemas estelares individuais para computadores específicos dentro do cluster.
- Outros MMOGs adotam arquiteturas mais distribuídas, nas quais o universo é particionado por um número potencialmente muito grande de **servidores**, os quais também pode estar **geograficamente distribuídos**. Então, os usuários são **alocados dinamicamente a um servidor** em particular com base nos padrões de utilização momentâneos e também pelos atrasos de rede até o servidor. 

---
### **1.2 Computação Móvel e Ubíqua**

A evolução da tecnologia permitiu a integração de dispositivos pequenos e portáteis em sistemas distribuídos, dando origem a dois conceitos inter-relacionados:

1. **Computação Móvel**: É a execução de tarefas de computação enquanto se desloca, permitindo que o usuário **acesse recursos de sua rede remota** ou **recursos locais** que encontra pelo caminho.
	- É preciso ter o reconhecimento de Localização. O desafio é lidar com a **conectividade variável** e manter o funcionamento apesar da mobilidade do dispositivo.

2. **Computação Ubíqua:** O **ambiente físico** está saturado de dispositivos computacionais pequenos e baratos (em carros, geladeiras, câmeras). A computação Ubíqua é o acesso a serviços de computação disponível em qualquer lugar e **transparente** (o usuário mal nota o computador, apenas sua função física).
    - Esses dispositivos precisam se **comunicar entre si** para criar um ambiente inteligente (ex: o celular controlando a máquina de lavar).
    - O principal problema prático é a **operação conjunta espontânea**, onde dispositivos de um visitante precisam **localizar e se associar rapidamente** a serviços locais que nunca usaram antes. Isso exige um mecanismo de **descoberta de serviço** rápido e conveniente.

---
### **1.3 Computação Distribuída como Serviço Público** 

A **Computação em Nuvem** é um modelo onde recursos de computação são fornecidos por terceiros e **alugados** ao usuário, em vez de serem de sua propriedade. O termo promove a visão de que a computação deve ser tão fácil de usar e pagar quanto a eletricidade ou a água. A Nuvem elimina a necessidade de o usuário ter muito software ou hardware local.

| Tipo de Recurso          | Exemplos                                                                                                                               |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| **Recursos Físicos**     | **Processamento:** Alugar poder computacional (nós virtuais/físicos). **Armazenamento:** Armazenamento remoto para arquivos e backups. |
| **Serviços de Software** | Software completo oferecido pela Internet (e-mail, calendários, aplicativos empresariais), como o Google Apps.                         |
![](attachments/Pasted%20image%2020250920075804.png)

- **Virtualização:** É crucial, pois permite que os fornecedores aluguem **nós virtuais** em vez de máquinas físicas. Isso oferece maior flexibilidade no gerenciamento dos recursos.    
- **Clusters de Computadores:** As nuvens são implementadas usando **clusters**. Um cluster consiste em computadores fracamente ou fortemente ligados que trabalham em conjunto, de modo que, em muitos aspectos, podem ser considerados como um único sistema. Clusters fornecem a **escala e o desempenho** necessários para atender a milhões de usuários.
- A Nuvem **reduz os requisitos de equipamento dos usuários**, permitindo que dispositivos portáteis e simples acessem uma vasta gama de recursos.
- O pagamento é frequentemente baseado na **utilização** (pago pelo que usar).

---
## **2. Desafios para sistemas distribuídos.**

### **2.1 Heterogeneidade**

A **heterogeneidade** (variedade de componentes) é um desafio central nos sistemas distribuídos. Ela se manifesta em quatro áreas principais:

1. **Redes:** Diferentes tipos de redes (Ethernet, Wi-Fi, etc.) são unificadas pelos **Protocolos Internet**
2. **Hardware e SO:** Computadores têm diferentes arquiteturas e sistemas operacionais.
3. **Linguagens de Programação:** Diferentes linguagens usam diferentes representações para dados e estruturas.
4. **Desenvolvimento:** Programas só se comunicam se seguirem **padrões comuns** (protocolos e representação de dados).

#### **2.1.1 Middleware**
O **Middleware** é a principal solução para mascarar a heterogeneidade. É uma camada de software que fornece uma **abstração de programação uniforme**, escondendo as diferenças de rede, hardware, SO e linguagens subjacentes.
#### **2.1.2 Migração de Código (Máquina Virtual)**
A **Migração de Código** visa resolver o problema de um programa executável ser geralmente amarrado a uma **arquitetura de hardware** e a um **Sistema Operacional** específicos. A **Máquina Virtual** é a solução para tornar o código portátil.

1. **Criação de Código Intermediário:** O compilador da linguagem (ex: Java, C#) não gera código de máquina nativo. Em vez disso, ele gera um **código intermediário**.
2. **VM como tradutor:** A Máquina Virtual (como o **CLR** do .NET) é um programa que atua como um **tradutor**. Ela é a única parte do sistema que é específica ao hardware e ao SO.
3. **Execução em Qualquer Lugar:** Para rodar o código, basta que o computador tenha a VM instalada. A VM recebe o código intermediário, entende o que ele precisa fazer e o **traduz** para o sistema específico.

---

### **2.2 Segurança**

A segurança em sistemas distribuídos é crucial devido ao alto valor dos recursos compartilhados e tem três componentes principais: **Confidencialidade** (proteção contra acesso não autorizado), **Integridade** (proteção contra alteração ou dano) e **Disponibilidade** (garantir acesso aos recursos).

1. **Comunicação Segura:** O principal desafio é enviar **informações sigilosas** pela rede. Isso exige **criptografia** para ocultar o conteúdo da mensagem.
2. **Identificação Confiável:** É fundamental **saber a identidade** do agente remoto. Isso é resolvido por **técnicas de criptografia** (como certificados digitais).
3. **Ataque de Negação de Serviço:** Um invasor **interrompe a disponibilidade** do serviço bombardeando-o com requisições sem sentido, impedindo que usuários legítimos o utilizem.

---
### **2.3 Escalabilidade**

A **escalabilidade** é a capacidade de um sistema distribuído permanecer eficiente diante de um aumento significativo no **número de usuários e recursos**.

Os principais desafios no projeto de sistemas escaláveis são:
1. **Controlar o Custo dos Recursos Físicos:** O custo para suportar n usuários deve se **proporcional** ao numero de máquinas. Se um servidor suporta 20 usuários, dois devem suportar 40. Isso exige a adição eficiente de servidores para evitar gargalos.
2. **Controlar a Perda de Desempenho:** O tempo de acesso aos dados não deve aumentar linearmente. Algoritmos devem usar **estruturas hierárquicas** (ex: DNS), onde a perda de desempenho é minimizada para **O(logn)**.
3. **Impedir o Esgotamento de Recursos de Software:** Deve-se prever a demanda futura para evitar que recursos de software críticos se esgotem (ex: o esgotamento dos endereços **IPv4** de 32 bits, exigindo a migração para **IPv6** de 128 bits).
4. **Evitar Gargalos de Desempenho:** Algoritmos e gerenciamento de dados devem ser **descentralizados**. O **DNS** resolveu o gargalo do sistema predecessor, que usava um único arquivo central, ao **particionar a tabela de nomes** entre diversos servidores distribuídos.

Técnicas essenciais para melhorar a escalabilidade incluem a **replicação de dados** e o uso de **cache** para recursos muito acessados.

---
### **2.4 Tratamento de Falhas**

As falhas em um sistema distribuído são parciais – isto é, alguns componentes falham, enquanto outros continuam funcionando. Portanto, o tratamento de falhas é particularmente difícil. 

**Detecção de falhas:** algumas falhas podem ser detectadas. Por exemplo, somas de verificação podem ser usadas para detectar dados corrompidos. O desafio é gerenciar a ocorrência de falhas que não podem ser detectadas.

**Mascaramento de falhas:** algumas falhas detectadas podem ser ocultas ou se tornar menos sérias. 
1. Mensagens podem ser retransmitidas quando não chegam. 
2. Dados podem ser gravados em dois discos, para que, se um estiver danificado, o outro ainda possa estar correto. 

**Tolerância a falhas**: a maioria dos serviços na Internet apresenta falhas. Seus clientes podem ser projetados de forma a tolerar falhas. Por exemplo, quando um navegador não consegue contatar um servidor Web, ele não faz o usuário esperar indefinidamente, ele informa o usuário sobre o problema, deixando-o livre para tentar novamente. 

**Redundância**: os serviços podem se tornar tolerantes a falhas com o uso de componentes redundantes. 
1. Sempre deve haver pelo menos duas rotas diferentes entre dois roteadores quaisquer na Internet. 
2. No Domain Name System, toda tabela de correspondência de nomes é replicada em pelo menos dois servidores diferentes. 
3. Um banco de dados pode ser replicado em vários servidores, para garantir que os dados permaneçam acessíveis após a falha de qualquer servidor.

Os sistemas distribuídos fornecem um alto grau de disponibilidade perante falhas de hardware. Quando um dos componentes de um sistema falha, apenas o trabalho que estava usando o componente defeituoso é afetado. Um usuário pode passar para outro computador, caso aquele que estava sendo utilizado falhe; um processo servidor pode ser iniciado em outro computador.