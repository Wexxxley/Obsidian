
#Concluded 

___
## **1. Exemplos e tendências** 
### **1.1 Massively multiplayer online games (MMOGs)**

A engenharia dos MMOGs representa um grande desafio para as tecnologias de sistemas distribuídos, devido à ==necessidade de tempos de resposta rápidos para preservar a experiência dos usuários do jogo==. Outros desafios incluem a ==propagação de eventos em tempo real para muitos jogadores e a manutenção de uma visão coerente== do mundo compartilhado. Foram propostas várias soluções para o projeto de MMOGs:

1. O jogo online, o EVE Online, utiliza uma **arquitetura cliente-servidor** na qual uma ==**única cópia do estado do mundo é mantida em um servidor centralizado e acessada por programas clientes em execução nos consoles dos jogadores**.== A arquitetura centralizada ajuda significativamente no gerenciamento do mundo virtual e a cópia única também diminui as preocupações com a coerência. Assim, o objetivo é garantir resposta rápida, para isso a carga é particionada por meio da alocação de sistemas estelares individuais para computadores específicos dentro do cluster.

2. Outros MMOGs adotam **arquiteturas mais distribuídas,** nas quais o universo é particionado por um número potencialmente muito grande de **servidores**, os quais também pode estar **geograficamente distribuídos**. Então, os usuários são **alocados dinamicamente a um servidor** em particular com base nos padrões de utilização momentâneos e também pelos atrasos de rede até o servidor. 

---
### **1.2 Computação Móvel e Ubíqua**

A evolução da tecnologia permitiu a integração de dispositivos pequenos e portáteis em sistemas distribuídos, dando origem a dois conceitos:

1. **Computação Móvel**: É a ==execução de tarefas de computação enquanto se desloca==, permitindo que o usuário **acesse recursos de sua rede** ou **recursos locais** que encontra pelo caminho.
	- É preciso ter o reconhecimento de Localização. O desafio é lidar com a **conectividade variável** e manter o funcionamento apesar da mobilidade do dispositivo.

2. **Computação Ubíqua:** O **ambiente físico** está saturado de dispositivos computacionais pequenos e baratos (em carros, geladeiras, câmeras). ==A computação Ubíqua é o acesso a serviços de computação disponível em qualquer lugar e **transparente**== (o usuário mal nota o computador, apenas sua função física).
    - Esses dispositivos precisam se **comunicar entre si** para criar um ambiente inteligente (ex: o celular controlando a máquina de lavar).
    - O principal problema prático é a **operação conjunta espontânea**, onde dispositivos de um visitante precisam **localizar e se associar rapidamente** a serviços locais que nunca usaram antes. Isso exige um mecanismo de **descoberta de serviço** rápido e conveniente.

---
### **1.3 Computação Distribuída como Serviço Público** 

A **Computação em Nuvem** é um ==modelo onde recursos de computação são fornecidos por terceiros e **alugados** ao usuário==, em vez de serem de sua propriedade. O termo promove a visão de que a computação deve ser tão fácil de usar e pagar quanto a eletricidade ou a água. A Nuvem elimina a necessidade de o usuário ter muito software ou hardware local.

| Recurso      | Exemplos                                                                                                                                |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| **Físicos**  | **Processamento:**Alugar poder computacional (nós virtuais/físicos).   **Armazenamento:** Armazenamento remoto para arquivos e backups. |
| **Software** | Software completo oferecido pela Internet (e-mail, calendários, aplicativos empresariais), como o Google Apps.                          |
![](attachments/Pasted%20image%2020250920075804.png)

- **Virtualização:** É crucial, pois permite que os fornecedores aluguem **nós virtuais** em vez de máquinas físicas. Isso oferece maior flexibilidade no gerenciamento dos recursos.    
- **Clusters de Computadores:** As nuvens são implementadas usando **clusters**. Um cluster consiste em computadores fracamente ou fortemente ligados que trabalham em conjunto, de modo que, em muitos aspectos, podem ser considerados como um único sistema. Clusters fornecem a **escala e o desempenho** necessários para atender a milhões de usuários.
- A Nuvem **reduz os requisitos de equipamento dos usuários**, permitindo que dispositivos portáteis e simples acessem uma vasta gama de recursos.
- O pagamento é frequentemente baseado na **utilização** (pago pelo que usar).


    
