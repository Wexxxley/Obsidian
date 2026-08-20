


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

>[!tip]
Para regras de negócio complexas seria interessante criar diagramas de atividades. Por exemplo: lógica de pagamento. Casos de estorno

---
O objetivo não vai ser validar a ideia (validada em empreendedorismo). 

**Stakeholders**: Não se limita ao financiador do projeto. É qualquer pessoa, grupo ou entidade que afete direta ou indiretamente o sistema, ou que seja afetado por ele.
- Usuários Finais Diretos.
- Usuários Internos: O adms do sistema.
- Idealizador: (eu) Papel de representante do negócio.

O objetivo da engenharia de requisitos com os TUTORES é mapear como o tutor buscará a informação e como o sistema deverá processar essas requisições.
- **Filtragem:** o tutor precisa filtrar cuidadores por geolocalização exata? porte do animal suportado? tipo de residência? disponibilidade em calendário.
- **Fluxos de Confiança:** Quais informações são essenciais para que você tome a desição de escolher um cuidador? Antecedentes criminais? fotos do ambiente?

---
### 2. Design Arquitetural e Modelagem

#### 2.1 Arquitetura
##### 2.1.1 Arquitetura Global 
Escolher arquitetura condizente com a proposta, sem Overengineering. Monolítico, microserviços, etc.

Independente do estilo global, o código-fonte também precisa ser organizado: Arquitetura em Camadas, Clean Architecture, etc. 
##### 2.1.2 Padrões de Comunicação
Define-se o protocolo e o contrato de como os módulos do sistema e as integrações com sistemas de terceiros trocarão informações. Comunicação Síncrona e Assíncrona. 
#### 2.2 Modelagem de Dados
- Modelagem
- Escolha do DB
#### 2.3 Modelagem Estrutural
- Utilização de notações gráficas, como o C4 Model, para representação visual da estutura. C4 model nivel 1 e 2 já são suficientes.
### 2.4 Prototipagem e Design de Interface
- **Wireframe:** Esboço preliminar da disposição dos elementos em tela e do caminho lógico. É preciso especificar as telas mais "ocultas", como as de backoffice.
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
- O desenvolvimento de um cliente web força o isolamento da lógica de negócios (API-First). Em uma evolução futura, o aplicativo móvel nativo atuaria apenas como um segundo cliente consumindo a mesma api.


---

Entrevistas estruturadas para Tutores e cuidadore (n precisa ser cuidadores que ja trabalham. "Se tal ferrramenta fosse desenvolvida, e vc se cadastrase para pretar serviços...")

Foco em ES, foco nas regras de negócio, foco nos requisitos n funcionais. e, com a arquitetura, desenvolver algo que atinja essa meta.

