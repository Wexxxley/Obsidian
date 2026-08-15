

---

Não existe o jeito certo de fazer software, mas tem que ter um balanço entre teoria e prática.
### **1. Concepção e Engenharia de Requisitos**

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
A validação do que foi especificado para garantir que a documentação reflete as necessidades.

>[!tip] Artefatos
>Especificação de requisitos.

---
### 2. Design Arquitetural e Modelagem

#### 2.1 Topologia Arquitetural
##### 2.1.1 Arquitetura Global 
- **Arquitetura Monolítica**
- **Arquitetura de Microsserviços**
- **Arquitetura Orientada a Eventos (Event-Driven)** 

Independente do estilo global escolhido, o código-fonte precisa ser organizado internamente. 
- **Arquitetura em Camadas:** Divisão tradicional onde o código é segmentado verticalmente (Apresentação, Lógica e Acesso a Dados). Uma camada superior só pode se comunicar com a camada imediatamente inferior.
- **Arquiteturas de Isolamento de Domínio:** Adoção de padrões como Clean Architecture ou Arquitetura Hexagonal. 
##### 2.1.2 Padrões de Comunicação
Define-se o protocolo e o contrato  de como os módulos do sistema e as integrações com sistemas de terceiros trocarão informações. Comunicação Síncrona  e Assíncrona. 
#### 2.2 Modelagem de Dados
- **Modelagem Conceitual e Lógica:** Criação do Modelo Entidade-Relacionamento, que define as entidades do sistema, seus atributos e as regras de cardinalidade.
- **Escolha do DB**.

#### 2.3 Modelagem Estrutural e Comportamental
- **Diagramação Arquitetural:** Utilização de notações gráficas, como o C4 Model, para representar a arquitetura em diferentes níveis de abstração hierárquica.

#### 2.4 Prototipagem e Design de Interface
- **Wireframe:** Esboço preliminar da disposição dos elementos em tela e do caminho lógico.
- **Prototipagem:** Construção de representações visuais fieis da interface final. Esta etapa define a paleta de cores, a tipografia e o mapeamento dos elementos visuais.

>[!tip] Artefatos
>- Registros de Decisões: Registram o contexto, a decisão técnica, diagramas.
>- Protótipo 


---
### **3. Construção e garantia de qualidade**

Geralmente, inicia-se pela implementação da lógica de negócios e da infraestrutura de dados (Backend), seguida pelo consumo dessas informações pelo Frontend. 

A garantia de qualidade ocorre paralelamente e logo após a construção de cada incremento do software. Esta macroetapa engloba a aplicação das rotinas de testes para garantir que a funcionalidade recém-criada opera sem erros e não quebra o código preexistente (regressão). 

---
### 4. Implantação e Análise de Métricas

A última macroetapa consiste em retirar o software do ambiente de desenvolvimento local e colocá-lo em um ambiente de produção. Aliado a isso, realiza-se a coleta de métricas de software (como o nível de complexidade ciclomática e a porcentagem de acoplamento do código final) para documentação.