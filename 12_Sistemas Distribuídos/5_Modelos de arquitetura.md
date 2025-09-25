

---
Enquanto os modelos físicos focam no hardware, os **modelos de arquitetura** descrevem um sistema em termos dos papéis computacionais e de comunicação desempenhados por seus componentes. ==A arquitetura de um sistema é a sua estrutura em termos de componentes e suas inter-relações==. 
## **1. Elementos Arquitetônicos**
Para entender os elementos fundamentais de um sistema distribuído é preciso examinar quatro questões principais:
##### **A. Entidades em Comunicação**
- **Do ponto de vista do sistema**, as entidades que se comunicam são geralmente os **processos**. Em ambientes mais complexos, podem ser as **threads** dentro dos processos.
- **Do ponto de vista da programação**, abstrações de nível mais alto são usadas para representar as entidades:
    - **Objetos**: Que são acessadas por meio de interfaces que definem seus métodos.
    - **Componentes**: Semelhantes aos objetos, mas com a diferença crucial de que especificam não apenas as interfaces que _fornecem_, mas também as que _exigem_ de outros componentes, tornando todas as suas dependências explícitas.
    - **Serviços Web**: Entidades encapsuladas e acessadas por meio de interfaces, mas que são intrinsecamente integradas à World Wide Web.

##### **B. Paradigmas de Comunicação**

1. **Comunicação entre Processos**: Refere-se a formas de comunicação de baixo nível, como a passagem de mensagens e a programação de soquetes, que dão acesso direto à API dos protocolos da Internet.

2. **Invocação Remota**: Paradigma mais comum em sistemas distribuídos e se baseia na comunicação entre duas entidades para invocar uma operação. As principais formas são:
    - **Protocolos de Requisição-Resposta**: Um par de mensagens (uma de requisição do cliente para o servidor, e outra de resposta do servidor para o cliente) que serve de base para a computação cliente-servidor.
    - **Chamada de Procedimento Remoto**: Permite que um procedimento em um processo remoto seja chamado como se fosse um procedimento local. O sistema de RPC oculta os detalhes da distribuição, como a passagem de mensagens e a codificação de parâmetros.
    - **Invocação de Método Remoto**: Similar à RPC, mas aplicada a objetos distribuídos. Um objeto pode invocar um método em um objeto remoto, e o sistema RMI pode suportar a passagem de referências de objetos como parâmetros.
        
3. **Comunicação Indireta**: A comunicação ocorre por meio de uma entidade intermediária, o que desacopla os remetentes dos destinatários. Isso proporciona:
    - **Desacoplamento Espacial**: O remetente não precisa conhecer a identidade do destinatário.
    - **Desacoplamento Temporal**: Remetente e destinatário não precisam existir ao mesmo tempo para se comunicar.
        
     As principais técnicas de comunicação indireta incluem:
	    - **Comunicação em Grupo**: Entrega de mensagens a um conjunto de destinatários que pertencem a um grupo.
	    - **Sistemas Publicar-Assinar**: Produtores (publicadores) distribuem eventos para consumidores (assinantes) por meio de um serviço intermediário.
	    - **Memória Compartilhada Distribuída (DSM)**: Fornece uma abstração de memória compartilhada para processos que não compartilham memória física

---
## **2. Arquitetura em Camadas**

Este é um dos padrões mais importantes e se manifesta de duas formas complementares:
#### **1. Camadas Lógicas**:
Este padrão organiza os serviços verticalmente em camadas de abstração. Cada camada utiliza os serviços da camada inferior, ocultando os detalhes de sua implementação. 
- **Plataforma**: As camadas de hardware e software de nível mais baixo, como o computador, a rede e o sistema operacional.
- **Middleware**: Uma camada de software que mascara a heterogeneidade da plataforma e fornece um modelo de programação mais conveniente para os desenvolvedores.
- **Aplicações e Serviços**: Camada superior que contém as aplicações utilizadas pelos users.

![500](attachments/Pasted%20image%2020250925183214.png)
#### **2. Camadas Físicas**
Este padrão foca na organização e no posicionamento da funcionalidade de uma camada lógica em servidores físicos distintos. Os modelos mais comuns são:
    
    - **Arquitetura de Duas Camadas**: A lógica da aplicação é dividida entre o cliente e um único servidor. Por exemplo, a lógica de apresentação fica no cliente e a lógica de dados e parte da aplicação ficam no servidor.
		- **Camada 1 (Cliente)**: O navegador Web (browser). Ele é responsável pela **lógica de apresentação**: renderiza o HTML, exibe as imagens e gerencia a interação do usuário
		- **Camada 2 (Servidor)**: O servidor Web (como Apache ou IIS). Ele é responsável tanto pela **lógica da aplicação** (encontrar o arquivo solicitado no sistema de arquivos do servidor) quanto pela **lógica de dados** (ler o arquivo do disco e enviá-lo pela rede).
        
    - **Arquitetura de Três Camadas**: A funcionalidade é dividida em três papéis lógicos, cada um geralmente mapeado para um servidor físico diferente: 1) Lógica de apresentação (cliente), 2) Lógica da aplicação (servidor de aplicação), e 3) Lógica de dados (servidor de banco de dados) . A enciclopédia Wikipedia é um exemplo de uma arquitetura de múltiplas camadas (n-camadas).
        
    - **AJAX (Asynchronous JavaScript and XML)**: O livro descreve o AJAX como uma técnica que aprimora a arquitetura em camadas na Web. Ele permite que programas JavaScript no navegador (cliente) solicitem novos dados diretamente de um programa no servidor e atualizem seletivamente partes de uma página Web, sem a necessidade de recarregar a página inteira . Isso resulta em aplicações Web mais rápidas e interativas, como o Google Maps.
        

#### **2. Clientes "Magros" (Thin Clients)**

Este padrão arquitetônico busca reduzir a complexidade do equipamento do usuário final, transferindo-a para os serviços da Internet.

- Um
    
    **cliente magro** é uma camada de software que suporta uma interface de usuário baseada em janelas localmente, enquanto executa os programas de aplicação em um computador remoto.
    
- A vantagem é que um dispositivo local simples (como um smartphone) pode acessar serviços e recursos de rede sofisticados.
    
- A tecnologia
    
    **VNC (Virtual Network Computing)** é um exemplo que implementa este conceito, permitindo o acesso remoto a interfaces gráficas de usuário ao transmitir eventos de teclado, vídeo e mouse pela rede.
    

#### **3. Outros Padrões Comuns**

- **Proxy**: Um objeto no espaço de endereçamento local que representa um objeto remoto. Sua função é tornar a invocação remota transparente para o cliente, encaminhando a chamada para o objeto remoto e retornando o resultado.
    
- **Brokerage (Corretagem)**: Usado em serviços Web, este padrão consiste em um trio: um provedor de serviço, um solicitante de serviço e um **corretor (broker)** que atua como um intermediário para conectar os dois.
    
- **Reflexão**: Um padrão que permite a um sistema examinar suas próprias propriedades dinamicamente (**introspecção**) e modificar sua estrutura ou comportamento dinamicamente (**intercessão**). Por exemplo, a RMI Java usa a introspecção para descobrir dinamicamente a interface de um objeto.