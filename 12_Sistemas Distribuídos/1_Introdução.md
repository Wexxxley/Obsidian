

---
### **1. O que é um Sistema Distribuído?**

Um **Sistema Distribuído** é uma coleção de **computadores independentes** (hardware e software) interligados por uma rede que **se comunicam e coordenam suas ações apenas através da troca de mensagens**.

Em termos simples: é um grupo de máquinas trabalhando juntas como se fossem um único sistema, mesmo estando separadas fisicamente.
## **2. Consequências Chave**

**Concorrência**: Se você tem um grande cálculo para fazer, o sistema pode distribuir esse cálculo por 100 máquinas, e todas trabalham nele ao mesmo tempo.  Se muitas pessoas acessam um site (como a Netflix), o sistema distribuído usa a concorrência para que milhares de servidores atendam a milhares de usuários **ao mesmo tempo**.

**Inexistência de Relógio Global**: Não existe um tempo único e perfeitamente sincronizado para todo o sistema. A coordenação entre os programas depende da troca de mensagens, e o tempo que essas mensagens levam na rede (latência) impede uma sincronização perfeita. Por isso, as ações são coordenadas por meio de **eventos** e **mensagens**, não por um relógio central.

**Falhas Independentes:** Componentes individuais (computadores, programas ou partes da rede) podem **falhar isoladamente** sem que todo o sistema pare. Quando uma máquina falha, as outras continuam operando. Os programas têm dificuldade em distinguir se um componente falhou ou se apenas a rede está lenta. Isso torna a **tolerância a falhas** um desafio e uma prioridade no projeto.

### **3. Exemplos Essenciais de Sistemas Distribuídos**

- **World Wide Web (WWW):** O maior sistema distribuído. Conteúdo (HTML, imagens) é espalhado por **milhões de servidores** e acessado via **navegadores** (clientes).
    
- **Mecanismos de Busca (Google, Bing):** Dividem o trabalho entre **_crawlers_** (coleta), **bancos de dados distribuídos** (armazenamento de índice) e **servidores de consulta** (resposta).
    
- **Redes Sociais (Meta, X):** Gerenciam **petabytes de dados** (posts, mídias) e **milhões de conexões** em múltiplos centros de dados para garantir escalabilidade.
    
- **Sistemas Bancários Online:** Garantem **consistência e segurança** de transações acessando dados em **servidores e bancos de dados geograficamente/logicamente distribuídos**.
    
- **E-commerce (Amazon, Mercado Livre):** Distribuem tarefas como **gerenciamento de inventário**, **pedidos** e **pagamentos** para suportar picos de tráfego.
    
- **Email e Mensagens (WhatsApp, SMTP):** Servidores **comunicam-se globalmente** para rotear e entregar mensagens, muitas vezes utilizando **infraestruturas distribuídas** para eficiência.
    
- **Streaming de Vídeo (Netflix, YouTube):** Utilizam **Redes de Entrega de Conteúdo (CDNs)** para copiar vídeos para **servidores próximos ao usuário**, otimizando a velocidade e a qualidade.
    
- **Rede de Escritório (LAN):** Exemplo básico onde **PCs** e **servidores de arquivos/impressão** se comunicam para compartilhar recursos.
    
- **Transferência Ponto a Ponto (Bluetooth/Wi-Fi):** Um sistema simples de **dois nós (celular/PC)** que coordenam uma ação (transferência de arquivo) por mensagens.
    
- **IoT Local (Sensores e Atuadores):** Dispositivos independentes (ex: sensor de temperatura e ar-condicionado) que **trocam mensagens** para alcançar um objetivo de automação.


### **Massively multiplayer online games (MMOGs)**
A engenharia dos MMOGs representa um grande desafio para as tecnologias de sistemas distribuídos, particularmente devido à necessidade de tempos de resposta rápidos para preservar a experiência dos usuários do jogo. Outros desafios incluem a propagação de eventos em tempo real para muitos jogadores e a manutenção de uma visão coerente do mundo compartilhado. Foram propostas várias soluções para o projeto de MMOGs:
- O jogo online, o EVE Online, utiliza uma arquitetura cliente-servidor na qual uma única cópia do estado do mundo é mantida em um servidor centralizado e acessada por programas clientes em execução nos consoles dos jogadores. O servidor é uma entidade complexa, consistindo em uma arquitetura de agregrado (cluster) caracterizada por centenas de nós de computador. A arquitetura centralizada ajuda significativamente no gerenciamento do mundo virtual e a cópia única também diminui as preocupações com a coerência. Assim, o objetivo é garantir resposta rápida, para isso a carga é particionada por meio da alocação de sistemas estelares individuais para computadores específicos dentro do cluster.

- Outros MMOGs adotam arquiteturas mais distribuídas, nas quais o universo é particionado por um número potencialmente muito grande de servidores, os quais também pode estar geograficamente distribuídos. Então, os usuários são alocados dinamicamente a um servidor em particular com base nos padrões de utilização momentâneos e também pelos atrasos de rede até o servidor. 

---
### **Computação Móvel e Ubíqua**
A evolução da tecnologia permitiu a integração de dispositivos pequenos e portáteis (como **smartphones**) em sistemas distribuídos, dando origem a dois conceitos inter-relacionados:

1. **Computação Móvel**: É a execução de tarefas de computação enquanto se desloca, permitindo que o usuário **acesse recursos de sua rede base (remota)** ou **recursos próximos (locais)** que encontra pelo caminho.
	- É preciso ter o reconhecimento de Localização. O desafio é lidar com a **conectividade variável** e manter o funcionamento apesar da mobilidade do dispositivo.

2. **Computação Ubíqua:** O **ambiente físico** está saturado de dispositivos computacionais pequenos e baratos (em carros, geladeiras, roupas). A computação Ubíqua é o acesso a serviços de computação disponível em qualquer lugar e **transparente** (o usuário mal nota o computador, apenas sua função física).
    - Esses dispositivos precisam se **comunicar entre si** para criar um ambiente inteligente (ex: o celular controlando a máquina de lavar).
    - O principal problema prático é a **operação conjunta espontânea**, onde dispositivos de um visitante (como uma câmera) precisam **localizar e se associar rapidamente** a serviços locais que nunca usaram antes (como a impressora da anfitriã). Isso exige um mecanismo de **descoberta de serviço** rápido e conveniente.

---
### **Computação Distribuída como Serviço Público** 

A **Computação em Nuvem** é um modelo onde recursos de tecnologia são fornecidos por terceiros (**fornecedores de serviço**) e **alugados** ao usuário, em vez de serem de sua propriedade. O termo promove a visão de que a computação deve ser tão fácil de usar e pagar quanto a eletricidade ou a água.

A Nuvem oferece recursos como um conjunto de serviços baseados na Internet, eliminando a necessidade de o usuário ter muito software ou hardware local.

| Tipo de Recurso          | Exemplos                                                                                                                                                                        |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Recursos Físicos**     | **Processamento:** Alugar poder computacional (nós virtuais/físicos). **Armazenamento:** Armazenamento remoto para arquivos, backups e grandes volumes de dados (data centers). |
| **Serviços de Software** | Software completo oferecido pela Internet (e-mail, calendários, aplicativos empresariais), como o Google Apps.                                                                  |

### 2. A Tecnologia de Base

- **Virtualização:** É crucial, pois permite que os fornecedores aluguem **nós virtuais** em vez de máquinas físicas. Isso oferece maior flexibilidade no gerenciamento dos recursos.
    
- **Clusters de Computadores:** As nuvens são implementadas usando **clusters** (conjuntos de computadores interligados, frequentemente usando hardware de prateleira ou servidores _blade_). Clusters fornecem a **escala e o desempenho** necessários para atender a milhões de usuários.
    

### 3. Impacto no Usuário

- A Nuvem **reduz os requisitos de equipamento dos usuários**, permitindo que dispositivos portáteis e simples acessem uma vasta gama de recursos.
    
- O pagamento é frequentemente baseado na **utilização** (pago pelo que usar), e não na aquisição de licenças ou hardware.


---
### **4. Motivação Principal**

A principal razão para construir e usar Sistemas Distribuídos é a necessidade de **compartilhar recursos**. Um **recurso** é um termo amplo que descreve qualquer item (hardware ou software) que possa ser usado ou acessado por múltiplos componentes (computadores, programas) interligados em uma rede.

Em essência, o sistema distribuído existe para permitir que recursos valiosos, que são caros ou escassos, sejam **acessados por muitos usuários ou máquinas de forma eficiente** 

#### **4.1 Exemplos de recursos Compartilhados em Sistemas Distribuídos**

| Recurso                        | Exemplo Prático de Compartilhamento                                                                                                                                                                    |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1. **Impressora de Rede**      | Em um escritório, todos os computadores estão conectados em rede. Quando alguém manda imprimir um documento, o trabalho de impressão é enviado para uma única impressora potente.                      |
| 2. **Disco rígido**            | Serviços como **Google Drive** ou **Dropbox**. Eles usam discos rígidos gigantescos em data centers para que milhões de usuários possam guardar suas fotos, documentos e vídeos num lugar seguro.      |
| 3. **CPU**                     | Uma empresa de animação tem dezenas de computadores. Para renderizar um filme eles usam o poder de processamento de todas as máquinas da rede ao mesmo tempo, terminando o trabalho muito mais rápido. |
| 4. **Câmera de Vídeo Digital** | Um **sistema de vigilância** onde **centenas de câmeras** em diferentes pontos transmitem seu fluxo de vídeo para um único servidor.                                                                   |
| 5. **Sensor**                  | Um **sistema IoT** onde um servidor monitora a temperatura e pressão relatadas por **sensores distribuídos**.                                                                                          |

| Recurso                            | Exemplo Prático de Compartilhamento                                                                                                                                                                              |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. **Banco de Dados**              | Um **sistema de e-commerce** onde o **catálogo de produtos** é replicado em vários servidores e acessado concorrentemente por **milhares de usuários** realizando consultas e pedidos.                           |
| 2. **Arquivos**                    | Uma plataforma de **colaboração em tempo real (ex: Google Docs)** onde o arquivo é o recurso principal e é modificado simultaneamente por **vários editores** em suas máquinas.                                  |
| 3. **APIs**                        | Uma api que compartilha seus recursos para vários usuários simultaneamente.                                                                                                                                      |
| 4. **Conexão de Voz **             | Uma no Zoom onde a conexão de áudio em tempo real é estabelecida e mantida entre **dois ou mais usuários** através de servidores intermediários.                                                                 |
| 5. **Software como Serviço SaaS)** | Usar um sistema online como **Gmail**, **Canva** ou **Netflix**. Você não precisa instalar o programa completo. Você só acessa o serviço pela internet (que roda em servidores distantes) e usa quando precisar. |
