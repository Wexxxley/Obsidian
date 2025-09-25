

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

1. **Arquitetura de Duas Camadas**: A lógica da aplicação é dividida entre o cliente e um servidor.
	- **Exemplo: Web**
		- **Camada 1**: Navegador Web . Ele é responsável pela **lógica de apresentação**: renderiza o HTML, exibe as imagens e gerencia a interação do usuário
		- **Camada 2**: Servidor Web. Ele é responsável tanto pela **lógica da aplicação** quanto pela **lógica de dados**.
	
2. **Arquitetura de Três Camadas**: A funcionalidade é dividida em três papéis lógicos, cada um geralmente mapeado para um servidor físico diferente: 1) Lógica de apresentação (cliente), 2) Lógica da aplicação (servidor de aplicação), e 3) Lógica de dados (servidor de banco de dados) 
	- **Exemplo: Uma loja online**
		- **Camada 1**: O navegador Web do usuário, que exibe os produtos.
		- **Camada 2**: O server Web que executa um programa que contém a lógica do negócio.
		- **Camada 3**: Um servidor de banco de dados (como PostgreSQL). O programa na camada de aplicação consulta ou atualiza este banco de dados para obter informações sobre produtos, registrar um novo pedido ou verificar os dados 

3. **AJAX (Asynchronous JavaScript and XML)**: Permite que programas JavaScript no navegador (cliente) solicitem novos dados diretamente de um programa no servidor e atualizem seletivamente partes de uma página Web, sem a necessidade de recarregar a página inteira.
	- **Exemplo: Google Maps**: Na interação Web tradicional, se você arrastasse o mapa para ver uma área adjacente, teria que esperar a página inteira ser recarregada com o novo mapa. Com AJAX, isso não acontece:
		- O mapa é exibido como um conjunto de pequenas imagens quadradas. 
		- Quando você move o mapa, o código JavaScript do navegador simplesmente reposiciona as áreas que já foram carregadas. Simultaneamente, o JavaScript faz chamadas em segundo plano (usando AJAX) para um servidor do Google, solicitando apenas as novas áreas necessárias para preencher os espaços vazios na tela.

---
## **3. Thin Clients**

Este padrão arquitetônico busca reduzir a complexidade do equipamento do usuário final, transferindo-a para os serviços da Internet.

- Um **cliente magro** é uma camada de software que suporta uma interface de usuário localmente, enquanto executa os programas de aplicação em um computador remoto.
- A vantagem é que um dispositivo local simples pode acessar serviços e recursos de rede sofisticados.

![](attachments/Pasted%20image%2020250925185406.png)

---
## **4. Soluções de Middleware**

**Middleware** é uma camada de software que fica acima da plataforma (SO e hardware) e abaixo das aplicações. Sua principal tarefa é fornecer uma abstração de programação de nível mais alto que simplifique o desenvolvimento de sistemas distribuídos. Ele faz isso mascarando a heterogeneidade da infraestrutura.

##### **Limitações do Middleware e o Princípio Fim-a-Fim**
Apesar de simplificar muito a programação, o middleware tem limitações. Nem todos os aspectos da confiabilidade e correção de um sistema podem ser totalmente abstraídos da aplicação. Para explicar isso, o capítulo apresenta o **princípio fim-a-fim** de Saltzer. A ideia central deste princípio é:

> Algumas funções relacionadas à comunicação só podem ser implementadas de forma completa com o conhecimento e a ajuda da aplicação que está nos pontos de extremidade (fim-a-fim). Portanto, fornecer essa função como um recurso do próprio sistema de comunicação (ou seja, no middleware) nem sempre é uma boa ideia.

Por exemplo, um serviço de transferência de e-mail não confia apenas na camada TCP para garantir a entrega de um arquivo muito grande. Se a conexão TCP for interrompida, o serviço de e-mail em si (a aplicação) mantém um registro do progresso e retoma a transmissão em uma nova conexão. A aplicação no ponto final é a única que pode garantir que a tarefa completa foi concluída com sucesso.



Certo, agora vamos para a última grande seção do capítulo.

### Parte 5: Modelos Fundamentais - O Modelo de Interação

#### **Introdução aos Modelos Fundamentais (Seção 2.4)**

Os **modelos fundamentais** adotam uma perspectiva mais abstrata para entender e analisar propriedades essenciais dos sistemas distribuídos. Seu objetivo é:

- Tornar explícitas todas as suposições relevantes sobre o sistema.
    
- Fazer generalizações sobre o que é possível ou impossível, dadas essas suposições.
    

O livro se concentra em três modelos fundamentais que examinam os aspectos de **interação**, **falhas** e **segurança**. Nesta parte, abordaremos o primeiro deles.

#### **O Modelo de Interação (Seção 2.4.1)**

Este modelo lida com o desempenho e a dificuldade de estabelecer limites de tempo em um sistema distribuído. Ele se concentra em dois fatores que afetam significativamente a interação entre processos:

1. **Desempenho da Comunicação**: A comunicação em uma rede tem as seguintes características de desempenho:
    
    - **Latência**: O atraso entre o início do envio de uma mensagem e o início de sua recepção no destino. Inclui o tempo de propagação do sinal, atrasos de acesso à rede e tempo de processamento nos sistemas operacionais.
        
    - **Largura de Banda (Bandwidth)**: O volume total de informações que pode ser transmitido por uma rede em um determinado momento.
        
    - **Jitter**: A variação no tempo necessário para entregar uma série de mensagens. É um fator crucial para dados de multimídia, como áudio e vídeo.
        
2. **Inexistência de Relógio Global**: Cada computador em um sistema distribuído tem seu próprio relógio interno, mas esses relógios se desviam uns dos outros com o tempo (um fenômeno chamado de **taxa de desvio do relógio** ou _drift_). É impossível sincronizá-los perfeitamente devido aos atrasos variáveis da rede. Isso significa que não existe uma noção global única de tempo, o que complica a coordenação de ações que dependem do tempo.
    

Com base nesses fatores, o modelo de interação se divide em duas variantes opostas:

- **Sistemas Distribuídos Síncronos**: Um sistema é síncrono se existem limites **conhecidos e finitos** para:
    
    - O tempo de execução de cada passo de um processo.
        
    - O tempo de entrega de cada mensagem transmitida.
        
    - A taxa de desvio do relógio de cada processo em relação ao tempo real.
        
        Embora seja difícil garantir esses limites na prática, modelar um sistema como síncrono é útil para analisar seu comportamento e permite, por exemplo, detectar falhas usando tempos limite (timeouts).
        
- **Sistemas Distribuídos Assíncronos**: Um sistema é assíncrono se **não existem limites** para a velocidade de execução dos processos, para os atrasos na transmissão de mensagens ou para as taxas de desvio do relógio. A Internet é um exemplo perfeito de um sistema assíncrono, pois uma mensagem de e-mail pode levar segundos ou dias para chegar. Muitas soluções para sistemas assíncronos também funcionam para sistemas síncronos, mas o contrário não é verdadeiro.
    

**Ordenação de Eventos**

Mesmo sem relógios perfeitamente sincronizados, é crucial saber se um evento (como o envio de uma mensagem) ocorreu antes de outro. O livro ilustra com um exemplo de e-mail (Figura 2.13), onde respostas podem chegar antes da mensagem original. Para resolver isso, **relógios lógicos** (propostos por Lamport) podem ser usados para fornecer uma ordenação de eventos que não depende de relógios físicos, mas sim da relação causal de que uma mensagem deve ser recebida após ter sido enviada.

A seguir, abordaremos o **Modelo de Falhas**.

Quando estiver pronto, digite **next**.

Ok, vamos para o próximo modelo.

### Parte 6: Modelos Fundamentais - O Modelo de Falhas

#### **O Modelo de Falhas (Seção 2.4.2)**

Este modelo define e classifica os diferentes tipos de falhas que podem ocorrer em um sistema distribuído. Ter uma classificação clara das falhas ajuda a analisar seus efeitos e a projetar sistemas que possam tolerá-las e continuar funcionando corretamente. O livro divide as falhas em três categorias principais:

1. **Falhas por Omissão (Omission Failures)**:
    
    - Ocorrem quando um processo ou canal de comunicação deixa de executar uma ação que deveria.
        
    - **Falha de Processo (Colapso / Crash)**: Um processo para e permanece parado. Outros processos podem ou não conseguir detectar esse estado. Se for possível detectar com certeza que o processo parou (por exemplo, em um sistema síncrono usando timeouts), a falha é chamada de **parada por falha (fail-stop)**.
        
    - **Falha de Comunicação**: Ocorre quando uma mensagem é perdida durante a transmissão entre o buffer de envio do remetente e o buffer de recepção do destinatário, o que é conhecido como "perda de mensagens".
        
2. **Falhas Arbitrárias (Arbitrary Failures)**:
    
    - Também conhecidas como **falhas Bizantinas**, representam o pior cenário de falha possível, onde qualquer tipo de erro pode ocorrer.
        
    - Um processo com falha arbitrária pode omitir passos, executar passos indesejados, atribuir valores incorretos aos seus dados ou retornar um valor errado em resposta a uma invocação.
        
    - Um canal de comunicação com falha arbitrária pode corromper mensagens, entregar mensagens inexistentes ou entregar a mesma mensagem mais de uma vez.
        
3. **Falhas de Temporização (Timing Failures)**:
    
    - Estas falhas são aplicáveis apenas a **sistemas síncronos**, onde existem limites de tempo definidos.
        
    - **Falha de Relógio**: O relógio local de um processo excede os limites de sua taxa de desvio em relação ao tempo real.
        
    - **Falha de Desempenho**: Um processo ou canal de comunicação excede os limites de tempo definidos para executar uma tarefa ou entregar uma mensagem.
        

#### **Tolerância e Mascaramento de Falhas**

Com base nesse modelo, podemos construir serviços mais confiáveis:

- **Mascaramento de Falhas**: Um serviço pode mascarar uma falha ocultando-a completamente ou convertendo-a em um tipo de falha mais aceitável. Por exemplo:
    
    - A retransmissão de mensagens pode mascarar a falha por omissão de um pacote perdido.
        
    - O uso de somas de verificação (checksums) pode converter uma falha arbitrária (mensagem corrompida) em uma falha por omissão (a mensagem corrompida é simplesmente descartada).
        
- **Comunicação Confiável**: Um serviço de comunicação é considerado confiável se possui duas propriedades:
    
    - **Validade**: Qualquer mensagem enviada é, eventualmente, entregue ao buffer de recepção do destino.
        
    - **Integridade**: A mensagem recebida é idêntica à enviada, e nenhuma mensagem é entregue duas vezes.
        

A seguir, abordaremos o último modelo fundamental: o **Modelo de Segurança**.

Quando estiver pronto, digite **next**.

Vamos para a parte final e conclusão do Capítulo 2.

### Parte 7: Modelos Fundamentais - O Modelo de Segurança

#### **O Modelo de Segurança (Seção 2.4.3)**

O modelo de segurança discute as possíveis ameaças aos processos e canais de comunicação e apresenta o conceito de um canal seguro para se proteger contra essas ameaças. A segurança de um sistema distribuído é obtida ao:

- Tornar seguros os processos e os canais usados para suas interações.
    
- Proteger os objetos que eles encapsulam contra o acesso não autorizado.
    

**Proteção de Objetos**

- **Direitos de Acesso**: Para proteger um recurso (como um objeto), o sistema especifica quem tem permissão para realizar determinadas operações sobre ele.
    
- **Principal**: Para gerenciar os direitos de acesso, o modelo introduz o conceito de **principal**, que é a identidade em nome da qual um processo está executando (geralmente um usuário ou outro processo). Um servidor é responsável por verificar a identidade do principal por trás de cada invocação e checar se ele tem direitos de acesso suficientes para a operação solicitada.
    

**Ameaças e o Invasor**

Para analisar as ameaças, o modelo postula a existência de um **invasor (atacante)** que é capaz de enviar qualquer mensagem para qualquer processo e ler ou copiar qualquer mensagem que trafega na rede. As principais ameaças são:

- **Ameaças aos Processos**: Como a origem de uma mensagem pode ser falsificada (spoofing), tanto servidores quanto clientes estão em risco.
    
    - Um **servidor** não pode ter certeza da identidade do principal por trás de uma requisição e pode, erroneamente, conceder acesso a um usuário não autorizado.
        
    - Um **cliente** não pode ter certeza de que uma mensagem de resposta veio do servidor correto; ela pode ter sido enviada por um invasor se passando pelo servidor.
        
- **Ameaças aos Canais de Comunicação**: Um invasor pode copiar, alterar ou injetar mensagens enquanto elas trafegam pela rede. Isso ameaça a **privacidade** (um invasor pode ler informações confidenciais) e a **integridade** (um invasor pode alterar o conteúdo de uma mensagem). Outro ataque é o de **replay**, onde um invasor salva mensagens e as reenvia mais tarde (por exemplo, reenviar uma requisição de transferência bancária).
    
- **Negação de Serviço (Denial of Service)**: Um ataque onde um usuário mal-intencionado impede que usuários legítimos utilizem um serviço, por exemplo, bombardeando o serviço com um número excessivo de requisições sem sentido.
    

**Anulando Ameaças com Canais Seguros**

As ameaças podem ser anuladas com o uso de **canais de comunicação seguros**. Um canal seguro é construído usando-se técnicas de criptografia e autenticação e possui as seguintes propriedades:

1. **Autenticação**: Cada um dos processos no canal conhece com certeza a identidade do principal em nome do qual o outro processo está executando.
    
2. **Privacidade e Integridade**: O canal garante a privacidade (por meio de criptografia para ocultar o conteúdo) e a integridade (proteção contra falsificação) dos dados transmitidos por ele.
    
3. **Proteção contra Replay**: Cada mensagem inclui uma indicação de tempo (lógico ou físico) para impedir que mensagens sejam reproduzidas ou reordenadas.
    

Com isso, concluímos a explanação do Capítulo 2, que apresentou os modelos físicos, de arquitetura e fundamentais, fornecendo as bases conceituais para entender o projeto de sistemas distribuídos.