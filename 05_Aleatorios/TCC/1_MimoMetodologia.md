


---
### **1. Engenharia de Requisitos**

#### **1.1 Elicitação de Requisitos**
- **Identificação de Stakeholders:** Mapeamento de todas as partes interessadas no sistema.
	- Ex: tutores de animais, cuidadores e o próprio administrador da plataforma.
- **Coleta de Dados:** Isso pode envolver entrevistas, análise de sistemas concorrentes, etc.
#### **1.2 Análise e Priorização**
- **Classificação:** Separação entre Requisitos Funcionais e Requisitos Não Funcionais.
- **Método MoSCoW:** Técnica de priorização dos requisitos para gerar o MVC.
#### **1.3 Especificação de Requisitos** 
Criação do documento, eliminando ambiguidades.
- **User Stories:** Descrição de funcionalidades sob a perspectiva do usuário final.
- **Critérios de Aceitação:** Estabelecimento de condições exatas e mensuráveis que o software deve satisfazer para que uma História de Usuário seja considerada concluída.
#### 1.4 Validação de Requisitos
A validação do que foi especificado para garantir que a documentação reflete as necessidades.

---
Meu objetivo nao vai ser validar a ideia (já foi validada na cadeira de empreendedorismo). A ideia é fazer uma elicitação de requisistos.

**Stakeholders**: não se limita ao financiador do projeto. É qualquer pessoa, grupo ou entidade que afete direta ou indiretamente o sistema, ou que seja afetado por ele.
- Usuários Finais Diretos.
- Usuários Internos: O adms do sistema.
- Stakeholders Tecnológicos: Sistemas de terceiros que integrarão com a plataforma, como gateways de pagamento ou serviços de envio de e-mail.
- Idealizador: (nesse cass, EU) Papel de representante do negócio.

O objetivo da engenharia de requisitos com os TUTORES é mapear como o tutor buscará a informação e como o sistema deverá processar essas requisições.
- **Filtragem:** o tutor precisa filtrar cuidadores por geolocalização exata? porte do animal suportado? tipo de residência? disponibilidade em calendário.
- **Fluxos de Confiança:** Quais informações são essenciais para que você tome a desição de escolher um cuidador? Antecedentes criminais? fotos do ambiente?

É preciso estudar os protocolos de em caso de problemas. Quais são as ações imediatas caso o animal adoeça?
- Encontrar pessoas que já façam esse trabalho de hospedar/cuidar de animais.
- Análise de Sistemas Similares

---
### 2. Design Arquitetural e Modelagem

#### 2.1 Arquitetura
##### 2.1.1 Arquitetura Global 
Escolher arquitetura condizente com a proposta, sem Overengineering. Monolítico, microserviços, etc.

Independente do estilo global, o código-fonte também precisa ser organizado: Arquitetura em Camadas, Clean Architecture, etc. 
##### 2.1.2 Padrões de Comunicação
Define-se o protocolo e o contrato de como os módulos do sistema e as integrações com sistemas de terceiros trocarão informações. Comunicação Síncrona e Assíncrona. 
#### 2.2 Modelagem de Dados
- **Modelagem Conceitual e Lógica:** Criação do Modelo Entidade-Relacionamento, que define as entidades do sistema, seus atributos e as regras de cardinalidade.
- **Escolha do DB**.
#### 2.3 Modelagem Estrutural
- **Diagramação Arquitetural:** Utilização de notações gráficas, como o C4 Model, para representar visual. C4 model nivel 1 e 2 já são suficientes.
### 2.4 Prototipagem e Design de Interface
- **Wireframe:** Esboço preliminar da disposição dos elementos em tela e do caminho lógico.
	- É preciso especificar as telas mais "ocultas", como a integração com backoffice.
- **Prototipagem:** Construção de representações visuais fieis da interface final. 

>[!tip] Artefatos
>- Registros de Decisões: Registram o contexto, a decisão técnica, diagramas.
>- Protótipo 

---
### **3. Construção, garantia de qualidade e análises**

- **Desenvolvimento de Backend e Qualidade de Código:** Foca na aplicação dos princípios SOLID, Object Calisthenics e boas práticas. Irei utilizarTDD. Depois irei calcular métricas de complexidade. Existem algumas ferramentas para isso.
    
- **Integrações Complexas:** O chat direto e o "Diário de Estadia" permite explorar a implementação de protocolos de comunicação bidirecional em tempo real, como WebSockets, e o gerenciamento de filas de processamento para o upload assíncrono de fotos e vídeos.
    
- **Análise de Desempenho:** Validar o projeto por meio da coleta de métricas de software. Como, análises do tempo de resposta dos endpoints da API, a latência na transmissão de mensagens do chat.

 
 **Justificativa versao web**
- Uma aplicação web responsiva já permite que tanto clientes com pcs e clientes mobile consigam acessar sem necessidade de donwload. E como é um MVP inicalmente.
- O desenvolvimento de um cliente web força o isolamento da lógica de negócios. A arquitetura "API-First". Em uma evolução futura, o aplicativo móvel nativo atuará apenas como um segundo cliente consumindo os mesmos recursos web.

---
### 4. Assuntos importantes a serem considerados

>[!tip]
**A armadilha do planejamento excessivo:** tentar prever tudo em um escopo fechado leva ao fracasso. O ideal é focar em uma MVP que possa ir ao ar rapidamente (2 a 4 meses), permitindo ajustar o produto com base no feedback real dos usuários.

>[!tip]
>Software não acaba: manutenção, atualização, sistema de suporte, atendimento....
#### 5.1 Integração com Backoffice
Refere-se a toda a **estrutura administrativa e operacional interna** de uma empresa que não possui contato direto com o cliente final. Enquanto o Frontoffice compreende as interfaces de usuário, o Backoffice engloba os setores e sistemas utilizados por funcionários internos para manter a empresa funcionando, como o setor de suporte técnico, processamento de pedidos, análise de crédito e TI. O próprio ERP é, frequentemente, o principal software utilizado.

**Backoffice Integrado vs. Separado**
Ambas as abordagens são aceitas na Engenharia de Software, mas possuem aplicações diferentes dependendo da escala do projeto.
- **Backoffice Integrado:** Abordagem ideal para MVPs e sistemas de pequeno a médio porte. O painel administrativo e a interface do cliente operam na mesma base de código, acessando o mesmo banco de dados. A separação ocorre pelo perfil de usuário.      
- **Backoffice Separado:** É a recomendação arquitetural padrão para sistemas de grande escala. O painel interno é construído como uma aplicação isolada, operando em servidores distintos e comunicando-se com o núcleo do sistema apenas através de rotas de API fechadas. A vantagem é o isolamento de falhas e a mitigação de ataques diretos

**Por exemplo, para a plataforma mimo**
- **Triagem de Cuidadores**: A operação mais crítica para garantir a confiança na plataforma. O administrador necessit+a de uma interface dedicada para analisar, aprovar ou rejeitar as documentações legais e os dados de contato submetidos pelos candidatos a cuidadores.
- **Gestão Transacional:** O backoffice deve monitorar o ciclo de vida dos pagamentos. Isso abrange a visualização dos valores retidos durante o agendamento, o processamento de estornos em caso de cancelamentos e a liberação formal do repasse financeiro para a conta bancária do cuidador após a conclusão da hospedagem ou do passeio.
- **Auditoria de Estadias:** A área operacional de suporte e intervenção técnica. Em casos de emergências veterinárias ou quebras de acordo de serviço, o administrador precisa acessar um painel com o histórico integral de ações. Isso inclui a auditoria do registro diário de estadia e o acesso ao registro de comunicação entre o tutor e o cuidador para mediar a situação com embasamento em dados.
- **Moderação do Sistema de Reputação**: A plataforma exige uma ferramenta para gerenciar as avaliações bidirecionais (as notas que os tutores dão aos cuidadores e vice-versa). A operação de backoffice consiste em auditar denúncias e ocultar comentários que contenham linguagem ofensiva ou fraudulenta, mantendo a integridade da pontuação pública dos usuários.
- **Suspensão e Banimento de Contas**: Uma operação de segurança sistêmica. Em casos de violação grave dos termos de serviço (como negligência por parte do cuidador ou inadimplência do tutor), o sistema de backoffice deve permitir o congelamento imediato dos perfis, impedindo novos logins e bloqueando a criação de novas contas com as mesmas credenciais.


