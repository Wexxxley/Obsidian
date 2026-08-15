

---

Não existe o jeito certo de fazer software, mas tem que ter um balanço entre teoria e prática.
### **1. Concepção e Engenharia de Requisitos**
Fase de definição do problema e do escopo. O objetivo não é detalhar todo o sistema, mas definir o que compõe o Mínimo Produto Viável (MVP). Nesta etapa, levantam-se os requisitos funcionais e os requisitos não funcionais. A saída desta macroetapa é um documento formal que dita exatamente o que precisa ser construído para a primeira versão da plataforma.
#### **1.1 Elicitação de Requisitos**
- **Identificação de Stakeholders:** Mapeamento de todas as partes interessadas no sistema.
	- Ex: tutores de animais, cuidadores e o próprio administrador da plataforma.
- **Coleta de Dados:** Utilização de écnicas de investigação para entender as restrições e regras de negócio. Isso pode envolver entrevistas, análise de sistemas concorrentes, etc.
#### **1.2 Análise e Priorização (Definição do MVP)**
- **Classificação:** Separação entre Requisitos Funcionais e Requisitos Não Funcionais.
- **Método MoSCoW:** Técnica de priorização dos requisitos.
#### **1.3 Especificação de Requisitos** 
Criação do documento, eliminando ambiguidades.
- **User Stories:** Descrição de funcionalidades sob a perspectiva do usuário final.
- **Critérios de Aceitação:** Estabelecimento de condições exatas e mensuráveis que o software deve satisfazer para que uma História de Usuário seja considerada concluída.
#### 1.4 Validação de Requisitos
A validação é a revisão formal do que foi especificado para garantir que a documentação reflete com precisão as necessidades reais e não possui contradições lógicas.

---
### 2. Design Arquitetural e Modelagem
Antes de escrever a primeira linha de código, a estrutura do sistema deve ser desenhada. É nesta macroetapa que ocorre a separação de responsabilidades. Define-se a topologia da arquitetura, a modelagem dos bancos de dados e a criação de protótipos visuais para as telas. 
### 2.1 Definição da Topologia Arquitetural
#### 2.1.1 Estilo Arquitetural Global 
- **Arquitetura Monolítica**
- **Arquitetura de Microsserviços**
- **Arquitetura Orientada a Eventos (Event-Driven)** 
### 2.1.2 Estruturação Lógica e Divisão em Camadas

Independente do estilo global escolhido acima, o código-fonte precisa ser organizado internamente. Esta subetapa define os padrões de projeto que ditarão as fronteiras e a separação de responsabilidades dentro do código.

- **Arquitetura em Camadas (N-Tier):** Divisão tradicional onde o código é segmentado verticalmente (geralmente em Apresentação, Lógica de Negócios e Acesso a Dados). Uma camada superior só pode se comunicar com a camada imediatamente inferior.
    
- **Arquiteturas de Isolamento de Domínio:** Adoção de padrões como a Arquitetura Limpa (_Clean Architecture_) ou Arquitetura Hexagonal (_Ports and Adapters_). O princípio central é que o núcleo do software (as regras de negócio puras) não deve conhecer nenhuma tecnologia externa (como o banco de dados ou a interface web). As dependências sempre apontam de fora para dentro.
    

### 2.1.3 Padrões de Comunicação e Integração

Nesta subetapa, define-se o protocolo e o contrato estrito de como os módulos do sistema e as integrações com sistemas de terceiros (como gateways de pagamento) trocarão informações.

- **Comunicação Síncrona:** O módulo que envia a requisição fica bloqueado aguardando uma resposta imediata do receptor. É modelada geralmente por meio de APIs RESTful (utilizando requisições HTTP padrão) ou gRPC (chamadas de procedimento remoto de alta performance).
    
- **Comunicação Assíncrona:** O módulo envia uma mensagem e continua seu processamento sem aguardar uma resposta imediata. É implementada utilizando intermediários de mensagens (_Message Brokers_, como RabbitMQ ou Apache Kafka). É fundamental para sistemas que precisam processar tarefas pesadas em segundo plano sem travar a interface do usuário.
    

### 2.1.4 Topologia de Infraestrutura e Implantação

A definição exata de onde e como o código será executado no ambiente de produção, estabelecendo as garantias de disponibilidade e tolerância a falhas.

- **Contêinerização:** O empacotamento do software e de todas as suas dependências (bibliotecas, configurações e compiladores) em unidades padronizadas (contêineres, como o Docker). Isso garante que o código funcionará da mesma forma no computador do desenvolvedor e no servidor final.
    
- **Orquestração e Nuvem:** Definição das ferramentas que gerenciarão a execução do sistema (como Kubernetes) e a escolha do provedor de computação em nuvem (_Cloud Computing_). Esta topologia define como o sistema criará cópias de si mesmo automaticamente (escalonamento horizontal) caso o tráfego de usuários aumente repentinamente.
    
#### 2.2 Modelagem de Dados
- **Modelagem Conceitual e Lógica:** Criação do Modelo Entidade-Relacionamento, que define as entidades do sistema, seus atributos e as regras de cardinalidade.
- **Escolha do DB**.

### 2.3 Modelagem Estrutural e Comportamental

O mapeamento visual de como o código-fonte será organizado e como as partes do sistema interagirão dinamicamente em tempo de execução.

- **Diagramação Arquitetural:** Utilização de notações gráficas formais, como o C4 Model, para representar a arquitetura em diferentes níveis de abstração hierárquica (Contexto de Sistema, Contêineres, Componentes e Código), facilitando a compreensão técnica da infraestrutura.
    
- **Mapeamento de Fluxos:** Elaboração de Diagramas de Sequência da Linguagem de Modelagem Unificada (UML) para detalhar a ordem cronológica exata das trocas de mensagens HTTP e chamadas de métodos durante processos críticos da plataforma, como o fluxo de agendamento de serviços ou o disparo de notificações.
    

### 2.4 Prototipagem e Design de Interface

A tradução visual dos requisitos levantados em telas funcionais, focando estritamente na experiência e na jornada interativa do usuário.

- **Wireframes e Fluxos de Navegação:** Esboço estrutural preliminar da disposição dos elementos em tela e do caminho lógico que o usuário percorre para concluir uma tarefa de ponta a ponta.
    
- **Prototipagem de Alta Fidelidade:** Construção de representações visuais exatas e interativas da interface final. Esta etapa define a paleta de cores, a tipografia e o mapeamento dos elementos visuais que guiarão a aplicação de bibliotecas de componentes responsivos durante a codificação.
    

### Artefatos Principais Gerados

Os documentos formais resultantes desta macroetapa estabelecem as bases para o início do desenvolvimento prático:

- **Registros de Decisões Arquiteturais (ADRs):** Documentos textuais padronizados que registram o contexto, a decisão técnica (como a escolha de um framework de interface ou padrão de projeto) e as consequências estruturais a longo prazo dessa adoção.
    
- **Diagrama Entidade-Relacionamento (DER):** A representação gráfica do esquema de persistência, evidenciando as chaves primárias, chaves estrangeiras e os vínculos estruturais entre as tabelas do banco de dados.
    
- **Documento de Arquitetura de Software:** O compilado técnico contendo os diagramas do C4 Model e os Diagramas de Sequência, formalizando a topologia e o comportamento do sistema.
    
- **Protótipos Validados:** O conjunto final de telas de alta fidelidade que servirá como um guia visual estrito e blueprint interativo para a fase de construção do frontend.
### 3. Construção Iterativa (Desenvolvimento)

Esta é a macroetapa da codificação pura, estruturada de forma progressiva. Seguindo uma abordagem adaptativa, a construção é fragmentada. Geralmente, inicia-se pela implementação da lógica de negócios e da infraestrutura de dados (Backend), seguida imediatamente pelo consumo dessas informações pela interface gráfica (Frontend). O foco aqui é manter a coesão do código e garantir que a interface em Vue.js opere de forma completamente isolada das regras centrais do servidor.

DDD? TDD? OUTRAS FORMAS?
### 4. Garantia de Qualidade e Validação Técnica

A validação técnica deve ocorrer paralelamente e logo após a construção de cada incremento do software. Esta macroetapa engloba a aplicação das rotinas de testes (como o Desenvolvimento Orientado a Testes - TDD, testes unitários e de integração) para garantir que a funcionalidade recém-criada opera sem erros e não quebra o código preexistente (regressão). O objetivo é garantir a estabilidade estrutural da plataforma.

  

### 5. Implantação e Análise de Métricas (Entrega)

A última macroetapa consiste em retirar o software do ambiente de desenvolvimento local e colocá-lo em um ambiente de produção (servidores em nuvem). Aliado a isso, realiza-se a coleta de métricas de software (como o nível de complexidade ciclomática e a porcentagem de acoplamento do código final) para documentação nos resultados do trabalho acadêmico. Após a entrega, o ciclo pode ser reiniciado para a adição de novas funcionalidades.

  

Qual destas cinco macroetapas você gostaria que fosse detalhada primeiro, expondo os processos e ferramentas específicos de suas etapas internas?
#### **Brainstorming Inicial (Não Técnico)**
A ideia é escrever livremente, como se estivesse conversando consigo mesmo, sobre como o sistema deve funcionar no geral. O objetivo é alinhar o entendimento do negócio e dos requisitos com o cliente.
#### **Detalhamento Técnico**
Aqui, o foco é técnico: como os campos funcionam, quais eventos ocorrem (cliques, chamadas de API), o que será processado e o que será retornado (ex: tokens JWT, armazenamento local). Isso serve para guiar o desenvolvedor ou a equipe técnica 
#### **Diagramação Visual:** 

Só agora, após ter os requisitos claros, parte-se para os diagramas. Um desenho simples em um papel com quadradinhos (tabelas) e setas (relacionamentos) já é suficiente para visualizar a estrutura do banco de dados.
#### **Escolha de tecnologias**

### Desenvolvimento

#### Cuidado com a segurança

#### Testes. Com tdd o sem