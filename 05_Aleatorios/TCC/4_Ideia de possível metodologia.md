

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
