
#Concluded 

---
### **1. O que é um Sistema Distribuído?**

Um **Sistema Distribuído** é uma ==coleção de **computadores independentes** interligados por uma rede que **se comunicam e coordenam suas ações apenas através da troca de mensagens**.==

Em termos simples: é um grupo de máquinas trabalhando juntas como se fossem um único sistema, mesmo estando separadas fisicamente.

---
## **2. Consequências Chave**

**Concorrência**: ==Se você tem um grande cálculo para fazer, o sistema pode distribuir esse cálculo por 100 máquinas==, e todas trabalham nele ao mesmo tempo.  Se muitas pessoas acessam um site (como a Netflix), o sistema distribuído usa a concorrência para que milhares de servidores atendam a milhares de usuários.

**Inexistência de Relógio Global**: ==Não existe um tempo único e perfeitamente sincronizado para todo o sistema==. A coordenação entre os programas depende da troca de mensagens, e o tempo que essas mensagens levam na rede (latência) impede uma sincronização perfeita. 

**Falhas Independentes:** Componentes individuais (computadores, programas ou partes da rede) podem **falhar isoladamente** sem que todo o sistema pare. Quando uma máquina falha, as outras continuam operando.

---
## **3. Exemplos de Sistemas Distribuídos**

- **World Wide Web (WWW):** O maior sistema distribuído. Conteúdo (HTML, imagens) é espalhado por **milhões de servidores** e acessado via **navegadores** (clientes).
    
- **Mecanismos de Busca (Google):** Dividem o trabalho entre **_crawlers_** (coleta), **bancos de dados distribuídos** (armazenamento de índice) e **servidores de consulta** (resposta).
    
- **Redes Sociais (Meta, X):** Gerenciam **petabytes de dados** (posts, mídias) e **milhões de conexões** em múltiplos centros de dados para garantir escalabilidade.
    
- **Sistemas Bancários Online:** Garantem **consistência e segurança** de transações acessando dados em **servidores e bancos de dados geograficamente/logicamente distribuídos**.
    
- **E-commerce (Amazon, Mercado Livre):** Distribuem tarefas como **gerenciamento de inventário**, **pedidos** e **pagamentos** para suportar picos de tráfego.
    
- **Email e Mensagens (WhatsApp, SMTP):** Servidores **comunicam-se globalmente** para rotear e entregar mensagens, muitas vezes utilizando **infraestruturas distribuídas** para eficiência.
    
- **Streaming de Vídeo (Netflix, YouTube):** Utilizam **Redes de Entrega de Conteúdo (CDNs)** para copiar vídeos para **servidores próximos ao usuário**, otimizando a velocidade e a qualidade.
    
- **Rede de Escritório (LAN):** Exemplo básico onde **PCs** e **servidores de arquivos/impressão** se comunicam para compartilhar recursos.
    
- **Transferência Ponto a Ponto (Bluetooth/Wi-Fi):** Um sistema simples de **dois nós (celular/PC)** que coordenam uma ação (transferência de arquivo) por mensagens.
    
- **IoT Local (Sensores e Atuadores):** Dispositivos independentes (ex: sensor de temperatura e ar-condicionado) que **trocam mensagens** para alcançar um objetivo de automação.

---
## **4. Motivação Principal**

A principal razão para construir e usar Sistemas Distribuídos é a ==necessidade de **compartilhar recursos**==. Um **recurso** é um termo amplo que descreve qualquer item (hardware ou software) que possa ser usado ou acessado por múltiplos componentes. Em essência, o sistema distribuído existe
para permitir que recursos valiosos, que são caros ou escassos, sejam **acessados por muitos usuários ou máquinas de forma eficiente** 

#### **4.1 Exemplos de recursos Compartilhados em Sistemas Distribuídos**

##### **Recursos de Hardware**

| Recurso                | Exemplo Prático                                                                                                                                                                                        |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1. **Impressora**      | Em um escritório, todos os computadores estão conectados em rede. Quando alguém manda imprimir um doc, o trabalho de impressão é enviado para uma única impressora.                                    |
| 2. **HD**              | Serviços como **Google Drive** ou **Dropbox** usam discos rígidos gigantescos em data centers para que milhões de usuários possam guardar suas fotos, documentos e vídeos num lugar seguro.            |
| 3. **CPU**             | Uma empresa de animação tem dezenas de computadores. Para renderizar um filme eles usam o poder de processamento de todas as máquinas da rede ao mesmo tempo, terminando o trabalho muito mais rápido. |
| 4. **Câmera de Vídeo** | Um **sistema de vigilância** onde **centenas de câmeras** em diferentes pontos transmitem seu fluxo de vídeo para um único servidor.                                                                   |
| 5. **Sensor**          | Um **sistema IoT** onde um servidor monitora a temperatura e pressão relatadas por **sensores distribuídos**.                                                                                          |
##### **Recursos de Software**

| Recurso                             | Exemplo Prático de Compartilhamento                                                                                                                                                                              |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. **Banco de Dados**               | Um **sistema de e-commerce** onde o **catálogo de produtos** é replicado em vários servidores e acessado concorrentemente por **milhares de usuários** realizando consultas.                                     |
| 2. **Arquivos**                     | Uma plataforma de **colaboração em tempo real (Google Docs)** onde o arquivo é o recurso principal e é modificado simultaneamente.                                                                               |
| 3. **APIs**                         | Uma api que compartilha seus recursos para vários usuários simultaneamente.                                                                                                                                      |
| 4. **Chamada **                     | Uma chamada no Zoom onde a conexão de áudio em tempo real é estabelecida e mantida entre **dois ou mais usuários** através de servidores intermediários.                                                         |
| 5. **Software como Serviço (SaaS)** | Usar um sistema online como **Gmail**, **Canva** ou **Netflix**. Você não precisa instalar o programa completo. Você só acessa o serviço pela internet (que roda em servidores distantes) e usa quando precisar. |

---
## **5 Transparência**

Transparência não é um desafio, mas sim uma característica de SD. A transparência é definida como a ==ocultação da separação dos componentes em um sistema distribuído, de modo que ele seja percebido como um todo.==

- **Transparência de Acesso**: ==Permite que recursos locais e remotos sejam acessados utilizando operações idênticas==. Por exemplo, usar as mesmas operações de leitura/escrita para um arquivo, não importando se ele está na máquina local ou em um servidor de arquivos remoto.
    
- **Transparência de Localização**: ==Permite que os recursos sejam acessados sem que se conheça sua localização física ou em rede.==
    
- **Transparência de Concorrência**: ==Permite que vários processos ou usuários acessem recursos compartilhados concorrentemente, sem que um interfira no outro.== O sistema gerencia o acesso concorrente para manter a consistência dos dados, e essa complexidade é oculta do usuário.
    
- **Transparência de Falhas**: ==Permite a ocultação de falhas, possibilitando que usuários e aplicações concluam suas tarefas apesar da falha de componentes de hardware ou software.== Um exemplo é o e-mail, que é entregue mesmo que um servidor ou um enlace de comunicação falhe temporariamente, pois o sistema tenta retransmitir as mensagens.
    
- **Transparência de Mobilidade**: Permite a movimentação de recursos e clientes dentro de um sistema sem afetar a operação de usuários ou programas. Um exemplo é o uso de telefones celulares, onde os usuários podem se mover de uma célula para outra durante uma chamada sem que a comunicação seja interrompida ou que eles percebam a mudança.
    
- **Transparência de Desempenho**: Permite que o sistema seja reconfigurado para melhorar o desempenho à medida que a carga de trabalho varia, sem que o usuário perceba.
    
- **Transparência de Escalabilidade**: Permite que o sistema e as aplicações se expandam em escala (adicionando mais usuários ou recursos) sem a necessidade de alterar a estrutura do sistema ou os algoritmos da aplicação.