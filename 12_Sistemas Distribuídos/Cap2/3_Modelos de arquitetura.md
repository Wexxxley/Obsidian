
#Concluded 

---
Enquanto os modelos físicos focam no hardware, os **modelos de arquitetura** descrevem um sistema em termos dos papéis computacionais e de comunicação desempenhados por seus componentes. ==A arquitetura de um sistema é a sua estrutura em termos de componentes e suas inter-relações==. 

---
## **1. Elementos Arquitetônicos**

##### **A. Entidades em Comunicação**
- **POV do sistema**, as entidades que se comunicam são geralmente os **processos**. 
- **POV da programação**, abstrações de nível mais alto são usadas para representar as entidades:
    - **Objetos**: Que são acessadas por meio de interfaces que definem seus métodos.
    - **Componentes**: Semelhantes aos objetos, mas com a diferença crucial de que especificam não apenas as interfaces que _fornecem_, mas também as que _exigem_ de outros componentes, tornando todas as suas dependências explícitas.
    - **Serviços Web**: Entidades encapsuladas e acessadas por meio de interfaces, mas que são intrinsecamente integradas à World Wide Web.

##### **B. Paradigmas de Comunicação**
1. **Comunicação entre Processos**: Refere-se a formas de comunicação de baixo nível, como a passagem de mensagens e a programação de soquetes.

2. **Invocação Remota**: Paradigma mais comum em sistemas distribuídos e se baseia na ==comunicação entre duas entidades para invocar uma operação==. As principais formas são:
    - **Protocolos de Requisição-Resposta**: Um par de mensagens que serve de base para a computação cliente-servidor.
    - **Chamada de Procedimento Remoto**: Permite que um procedimento em um processo remoto seja chamado como se fosse um procedimento local. O sistema de RPC oculta os detalhes da distribuição, como a passagem de mensagens e a codificação de parâmetros.
    - **Invocação de Método Remoto**: Similar à RPC, mas aplicada a objetos distribuídos. Um objeto pode invocar um método em um objeto remoto, e o sistema RMI pode suportar a passagem de referências de objetos como parâmetros.

3. **Comunicação Indireta**: ==A comunicação ocorre por meio de uma entidade intermediária==, o que desacopla os remetentes dos destinatários. Isso proporciona:
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

1. **Arquitetura de Duas Camadas**: A lógica da aplicação é dividida entre o ==cliente e um servidor.==
	- **Exemplo: Web**
		- **Camada 1**: Navegador Web . Ele é responsável pela **lógica de apresentação**: renderiza o HTML, exibe as imagens e gerencia a interação do usuário
		- **Camada 2**: Servidor Web. Ele é responsável tanto pela **lógica da aplicação** quanto pela **lógica de dados**.
	
2. **Arquitetura de Três Camadas**: A funcionalidade é dividida em três papéis, cada um mapeado para um servidor físico diferente: ==1) Lógica de apresentação (cliente), 2) Lógica da aplicação (servidor de aplicação), e 3) Lógica de dados (servidor de banco de dados)== 
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

- Um **cliente magro** é uma ==camada de software que suporta uma interface de usuário localmente, enquanto executa os programas de aplicação em um computador remoto.==
- A vantagem é que um dispositivo local simples pode acessar serviços e recursos de rede sofisticados.

![](attachments/Pasted%20image%2020250925185406.png)

---
## **4. Soluções de Middleware**

**Middleware** é uma camada de software que fica acima da plataforma (SO e hardware) e abaixo das aplicações. Sua principal tarefa é ==fornecer uma abstração de programação de nível mais alto que simplifique o desenvolvimento de sistemas distribuídos. Ele faz isso mascarando a heterogeneidade da infraestrutura.==

##### **Limitações do Middleware e o Princípio Fim-a-Fim**
Apesar de simplificar muito a programação, o middleware tem limitações. Nem todos os aspectos da confiabilidade e correção de um sistema podem ser totalmente abstraídos da aplicação. Para explicar isso, o capítulo apresenta o **princípio fim-a-fim** de Saltzer. A ideia central deste princípio é:

> ==Algumas funções relacionadas à comunicação só podem ser implementadas de forma completa com o conhecimento e a ajuda da aplicação que está nos pontos de extremidade (fim-a-fim).== Portanto, fornecer essa função como um recurso do próprio sistema de comunicação (ou seja, no middleware) nem sempre é uma boa ideia.

Por exemplo, um serviço de transferência de e-mail não confia apenas na camada TCP para garantir a entrega de um arquivo muito grande. Se a conexão TCP for interrompida, o serviço de e-mail em si (a aplicação) mantém um registro do progresso e retoma a transmissão em uma nova conexão. A aplicação no ponto final é a única que pode garantir que a tarefa completa foi concluída com sucesso.
