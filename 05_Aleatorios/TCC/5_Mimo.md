

---
### TCC 1: Concepção, Arquitetura e Produto Mínimo Viável (MVP)

- **Metodologia e Processo de Desenvolvimento:** O trabalho deve definir e justificar formalmente o ciclo de vida de software adotado para o desenvolvimento do projeto.
- A pesquisa abordará a escolha de um processo iterativo e incremental, detalhando as práticas de engenharia empregadas.
- Isso inclui a definição de estratégias de versionamento de código, gestão de ramificações (branching models) e o planejamento da integração contínua do código-fonte.
- O objetivo é demonstrar academicamente como o desenvolvimento será gerenciado para mitigar riscos técnicos e garantir a entrega contínua de funcionalidades testáveis.

- **Engenharia de Requisitos:** Nesta etapa, as validações de mercado levantadas no projeto original serão traduzidas para a linguagem formal da Engenharia de Software.
- O documento apresentará a elicitação de requisitos utilizando a técnica de Histórias de Usuário (User Stories), detalhando formalmente os Critérios de Aceite para cada funcionalidade prevista.
- MoSCoW: técnic para justificar metodicamente quais requisitos compõem estritamente o Produto Mínimo Viável (MVP) e quais serão postergados.
- A análise incluirá o mapeamento dos requisitos não funcionais, estabelecendo métricas exatas para segurança, desempenho (tempo máximo de resposta da API) e usabilidade.

- **Modelagem Estrutural e Comportamental:** Antes da implementação, o software deve ser rigorosamente modelado para prever o comportamento dos componentes e a comunicação entre as partes do sistema.
- **C4 Model:** técnica de notação gráfica para modelar a arquitetura de software de forma hierárquica. 
- Para os fluxos de dados mais complexos, como o sistema de aprovação de estadias e o envio de relatórios diários, o trabalho pode usar Diagramas de Sequência da UML. Esses diagramas mapearão a ordem exata das chamadas de métodos e as respostas HTTP entre o cliente (aplicativo) e o servidor (API RESTful).

- **Documentação de Decisões Arquiteturais (ADRs)**: Na Engenharia de Software moderna, as escolhas tecnológicas devem ser formalmente justificadas e registradas.
- Architecture Decision Records (ADRs). Um ADR é um documento formal que captura o contexto de uma decisão técnica, a decisão em si e as consequências dessa adoção. Serão redigidos ADRs para justificar academicamente a adoção da Arquitetura Limpa (Clean Architecture), o uso do padrão Model-View-ViewModel (MVVM) no aplicativo móvel e a escolha das linguagens e frameworks.
### Engenharia de Usabilidade e Interface
- As telas e os fluxos de navegação desenhados no protótipo passarão por uma Avaliação Heurística. Este é um método de inspeção de usabilidade onde especialistas analisam a interface com base em princípios consolidados, como as Dez Heurísticas de Nielsen.
- O trabalho formalizará a análise de aspectos como a visibilidade do status do sistema (explicando como o usuário saberá se uma foto do pet foi enviada com sucesso) e a prevenção de erros na entrada de dados durante o cadastro de um animal.
### TCC 2: Implementação Avançada, Integrações e Validação Técnica
O segundo trabalho absorve a base arquitetural estabelecida no TCC 1 e foca na resolução de problemas de software mais complexos, na garantia de qualidade e na validação das métricas técnicas do produto final.

- **Desenvolvimento de Backend e Qualidade de Código:** Codificar a API RESTful completa da plataforma. O referencial teórico e prático desta etapa deve focar na aplicação rigorosa dos princípios SOLID e nas regras de Object Calisthenics (regras de design orientado a objetos que visam manter o código coeso e de fácil manutenção), garantindo que a API seja facilmente testável e escalável, independentemente da linguagem escolhida (C#, Python ou Node.js).
    
- **Implementação de Integrações Complexas:** Desenvolver a infraestrutura técnica para o funcionamento do chat direto e do "Diário de Estadia". Academicamente, isso permite explorar a implementação de protocolos de comunicação bidirecional em tempo real, como WebSockets, e o gerenciamento eficiente de filas de processamento para o upload assíncrono de fotos e vídeos.
    
- **Garantia de Qualidade de Software (Testes):** Estruturar uma suíte de testes automatizados. O documento detalhará a implementação de testes unitários para isolar e validar as regras de negócio da API e testes de integração e interface (instrumentação) para validar o comportamento dos componentes nativos no ambiente Android.
    
- **Análise de Desempenho e Resultados:** Validar o projeto por meio da coleta de métricas de software. A monografia final apresentará análises do tempo de resposta dos endpoints da API, a latência na transmissão de mensagens do chat e a eficiência do uso de memória do aplicativo móvel nos dispositivos finais.


---
 
 **Justificativa versao web**

- Uma aplicação web responsiva já permite que tanto clientes com pcs como cleintes mobile consigam acessar sem necessidade de donwload. E como é um MVP inicalmente

- O desenvolvimento de um cliente web força o isolamento da lógica de negócios. A arquitetura "API-First". Em uma evolução futura, o aplicativo móvel nativo atuará apenas como um segundo cliente consumindo os mesmos recursos web.