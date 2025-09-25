

---
Mostramos como as **propriedades** e os **problemas** de projeto de sistemas distribuídos **podem ser capturados e discutidos por meio do uso de modelos descritivos**. Cada tipo de modelo é destinado a fornecer uma descrição abstrata e simplificada de um aspecto relevante.

1. Os **modelos físicos** são a maneira mais explítica de descrever um sistema; eles capturam a composição de hardware de um sistema, em termos dos computadores e suas redes de interconexão.

2. Os **modelos de arquitetura** descrevem um sistema em termos das tarefas computacionais e de comunicação realizadas por seus elementos computacionais – os computadores individuais ou seus agregados (clusters) suportados pelas interconexões de rede apropriadas.

3. Os **modelos fundamentais** adotam uma perspectiva abstrata para examinar os aspectos individuais de um sistema distribuído.
	1. **modelos de interação**, que consideram a estrutura e a ordenação da comunicação entre os elementos do sistema; 
	2. **modelos de falha,** que consideram as maneiras pelas quais um sistema pode deixar de funcionar corretamente;
	3. **modelos de segurança**, que consideram como o sistema está protegido contra tentativas de interferência em seu funcionamento correto ou de roubo de seus dados.

---
## **1. Modelos físico**

#### **1.1 Modelo físico básico**: 
Um modelo físico básico é um ==conjunto extensível de nós de computador interconectados por uma rede de computadores para troca de mensagens.==

**Sistemas distribuídos primitivos**: Surgiram no início dos anos 1980 em resposta ao surgimento da tecnologia de redes locais. Esses sistemas consistiam em algo entre 10 e 100 nós interconectados por uma ==rede local, suportando uma pequena variedade de serviços==, como impressoras, servidores de arquivos compartilhados,  e transferências de e-mail. Não havia muita preocupação com o fato de serem abertos. 
#### **1.2 Sistemas distribuídos adaptados para a Internet:**
Aproveitando essa base, S.D de maior escala começaram a surgir nos anos 1990, em resposta crescimento da Internet. Nesses sistemas, a infraestrutura consiste em um modelo que é um ==conjunto extensí-vel de nós interconectados por uma rede de redes. Esses sistemas exploravam a infraestrutura oferecida pela Internet para desenvolver sistemas distribuídos realmente globais==, envolvendo potencialmente grandes números de nós.  Como resultado, o nível de **heterogeneidade** nesses sistemas era significativo em termos de redes, arquiteturas de computador, sistemas operacionais, linguagens e também equipes de desenvolvimento envolvidas. Isso levou a uma ênfase cada vez maior em padrões abertos e tecnologias de middleware associadas.
#### **1.3 Sistemas distribuídos contemporâneos:**
Nos sistemas anteriores, os nós normalmente eram relativamente **estáticos**, **separados** e **autônomos**. As principais tendências que resultaram em desenvolvimentos significativos nos modelo físicos são:
1. A **computação móvel** levou a modelos físicos em que nós como smartphones podem mudar de um lugar, levando à necessidade de mais recursos, como a descoberta de serviço e o suporte para operação conjunta espontânea.
2. A **computação ubíqua** levou à mudança de nós distintos para arquiteturas em que os computadores são incorporados em objetos comuns e no ambiente circundante.
3. A **computação em nuvem** e, em particular, das arquiteturas de agregados (clusters), levou a uma mudança de nós autônomos para conjuntos de nós que, juntos, fornecem determinado serviço.
#### **1.4 Sistemas distribuídos de sistemas:**
Um sistema de sistemas pode ser definido como um sistema complexo, consistindo em uma série de subsistemas, os quais são, eles próprios, sistemas que se reúnem para executar uma ou mais tarefas em particular.

Como exemplo de sistema de sistemas, considere um sistema de gerenciamento ambiental para previsão de enchentes. Nesse cenário, existirão redes de sensores implantadas para monitorar o estado de vários parâmetros ambientais; Isso pode, então, ser acoplado a sistemas responsáveis por prever a probabilidade de enchentes, fazendo simulações em clusters. Outros sistemas podem ser estabelecidos para manter e analisar dados históricos .

---
## **2. Modelos de arquitetura** 

Enquanto os modelos físicos focam no hardware, os **modelos de arquitetura** descrevem um sistema em termos dos papéis computacionais e de comunicação desempenhados por seus componentes. ==A arquitetura de um sistema é a sua estrutura em termos de componentes e suas inter-relações==. 
#### **1. Elementos Arquitetônicos**
Para entender os elementos fundamentais de um sistema distribuído é preciso examinar quatro questões principais:
##### **A. Entidades em Comunicação**
- **Do ponto de vista do sistema**, as entidades que se comunicam são geralmente os **processos**. Em ambientes mais complexos, podem ser as **threads** dentro dos processos.
- **Do ponto de vista da programação**, abstrações de nível mais alto são usadas para representar as entidades:
    - **Objetos**: Unidades naturais de decomposição para um problema, acessadas por meio de interfaces que definem seus métodos.
    - **Componentes**: Semelhantes aos objetos, mas com a diferença crucial de que especificam não apenas as interfaces que _fornecem_, mas também as que _exigem_ de outros componentes, tornando todas as suas dependências explícitas.
    - **Serviços Web**: Entidades encapsuladas e acessadas por meio de interfaces, mas que são intrinsecamente integradas à World Wide Web, usando padrões como XML para representação e descoberta.

##### **B. Paradigmas de Comunicação (Como se comunicam?)**

O livro descreve três tipos principais de paradigmas de comunicação:

1. **Comunicação entre Processos**: Refere-se a formas de comunicação de baixo nível, como a passagem de mensagens e a programação de soquetes, que dão acesso direto à API dos protocolos da Internet.
    
2. **Invocação Remota**: É o paradigma mais comum em sistemas distribuídos e se baseia na comunicação entre duas entidades para invocar uma operação em um local remoto. As principais formas são:
    
    - **Protocolos de Requisição-Resposta**: Um par de mensagens (uma de requisição do cliente para o servidor, e outra de resposta do servidor para o cliente) que serve de base para a computação cliente-servidor.
        
    - **Chamada de Procedimento Remoto (RPC)**: Permite que um procedimento em um processo remoto seja chamado como se fosse um procedimento local. O sistema de RPC oculta os detalhes da distribuição, como a passagem de mensagens e a codificação de parâmetros.
        
    - **Invocação de Método Remoto (RMI)**: Similar à RPC, mas aplicada a objetos distribuídos. Um objeto pode invocar um método em um objeto remoto, e o sistema RMI pode suportar a passagem de referências de objetos como parâmetros.
        
3. **Comunicação Indireta**: A comunicação ocorre por meio de uma entidade intermediária, o que desacopla os remetentes dos destinatários. Isso proporciona:
    
    - **Desacoplamento Espacial**: O remetente não precisa conhecer a identidade do(s) destinatário(s).
        
    - **Desacoplamento Temporal**: Remetente e destinatário(s) não precisam existir ao mesmo tempo para se comunicar.
        
        As principais técnicas de comunicação indireta incluem:
        
    - **Comunicação em Grupo**: Entrega de mensagens a um conjunto de destinatários que pertencem a um grupo.
        
    - **Sistemas Publicar-Assinar**: Produtores (publicadores) distribuem eventos para consumidores (assinantes) por meio de um serviço intermediário.
        
    - **Filas de Mensagem**: Processos produtores enviam mensagens para uma fila específica, e processos consumidores as retiram da fila.
        
    - **Espaços de Tupla**: Processos colocam itens de dados estruturados (tuplas) em um espaço persistente, e outros processos podem ler ou remover essas tuplas especificando padrões de interesse.
        
    - **Memória Compartilhada Distribuída (DSM)**: Fornece uma abstração de memória compartilhada para processos que não compartilham memória física, permitindo que leiam e escrevam em estruturas de dados como se estivessem em seu próprio espaço de endereçamento local.