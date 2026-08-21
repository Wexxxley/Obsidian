

---

### **1. Pagamento com Retenção em Custódia**

- **Estados da Transação:** O banco de dados precisará gerenciar um ciclo de vida para os pedidos (ex: `CRIADO`, `PAGO_RETIDO`, `EM_ANDAMENTO`, `CONCLUIDO_LIBERADO`, `ESTORNADO`).
    
- **Rotinas de Webhooks e Resiliência:** A plataforma deve implementar endpoints para escutar eventos assíncronos enviados pelo gateway (confirmação de pagamento, falhas de repasse e liquidações), garantindo que o status no banco de dados esteja sempre sincronizado.
    
- **Tratamento de Exceções e Mediação:** O módulo de Backoffice precisará de ferramentas para desbloqueio manual ou estorno caso ocorra uma contestação ou disputa entre o tutor e o cuidador.
### 2. Responsabilidade legal do cuidador 

No ordenamento jurídico brasileiro, ao receber o animal, o cuidador e o tutor firmam um "Contrato de Depósito". A plataforma atua apenas como intermediadora de tecnologia e pagamentos. Ao assumir a posse do animal, o cuidador torna-se o guardião temporário, assumindo a responsabilidade civil e criminal por danos, fugas ou negligência, enquanto o tutor mantém a responsabilidade por condições de saúde naturais e preexistentes.

**1. Formalização da Responsabilidade Legal no Software**
- **Termo de Guarda Temporária digital:** Deve haver uma etapa de aceite explícito de um Termo de Responsabilidade. O sistema precisa registrar o evento de aceite no banco de dados, gravando o timestamp, o endereço IP do usuário e a versão específica do documento.
- **Isenção Médica Específica:** O contrato digital embutido no sistema deve deixar claro que custos com doenças naturais ou genéticas são de responsabilidade do tutor. 

**2. Protocolo para Emergências Veterinárias (Doenças Naturais)**
- Durante a estadia, o cuidador precisa ter acesso rápido aos dados de saúde do pet. O sistema deve congelar as informações da ficha clínica no momento do check-in, impedindo mudanças.
- O cuidador deve agir com diligência (prestar socorro). O aplicativo deve possuir um "Botão de SOS" na tela da reserva ativa. Ao acionar essa rota na API, o sistema altera o status da reserva para alerta, dispara notificações _Push_ de alta prioridade para o tutor e registra no banco de dados que o cuidador cumpriu seu dever de informar imediatamente.
- Caso o cuidador precise pagar um atendimento de urgência do próprio bolso, o sistema deve permitir o anexo de notas fiscais veterinárias dentro do histórico da estadia para que o tutor realize o reembolso, mediado pelo módulo de Backoffice.
### 3. Fuga, Maus-Tratos ou Apropriação Indébita
- Como o cuidador assume a responsabilidade civil e criminal, a plataforma não pode permitir perfis não verificados. A arquitetura de software deve exigir o envio de frente e verso do RG/CNH e uma foto do rosto. O sistema valida essas informações (manualmente no Backoffice ou via APIs de terceiros) antes de mudar o status do usuário para `APROVADO`.      
- O sistema deve armazenar as fotos, as mensagens do chat e os registros de horários de forma estruturada. Se o cuidador alegar que o cachorro fugiu por acidente, a frequência das atualizações e as imagens do portão/casa servirão como prova para determinar se houve negligência.
- Em caso de denúncia de fuga, roubo ou agressão, o sistema aciona automaticamente o bloqueio dos valores. O montante pago pelo tutor permanece retido na subconta do gateway de pagamento, impedindo que o cuidador receba o lucro do serviço até que a investigação seja encerrada.

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

---
### **5. Antecedentes criminais**

Existem diversas APIs no mercado que realizam a consulta de antecedentes criminais e a validação de identidade. Como a emissão de certidões criminais no Brasil é descentralizada (dividida entre Polícia Federal, Polícias Civis estaduais e diversos Tribunais de Justiça), existem softwares privados que automatizam essa varredura em órgãos públicos.

A legislação brasileira classifica os antecedentes criminais, biometria e dados de saúde como **Dados Pessoais Sensíveis**.
- O seu sistema não pode realizar a chamada para a API de antecedentes criminais sem que o cuidador saiba. A interface gráfica do aplicativo deve possuir uma tela com um aceite explícito onde o usuário autoriza a plataforma a coletar e consultar seus antecedentes criminais.
- O banco de dados não deve armazenar os detalhes dos crimes ou processos que a API retornar. O correto é processar a aprovação ou rejeição na memória do servidor e armazenar no banco apenas o status da validação (Ex: `background_check_passed: true` e a data da checagem).

Para fins acadêmicos pode-se utilizar um Mock. Detalhando que, em um ambiente de produção, aquele serviço simulado será substituído por uma API real.


---

### 6. Fluxo de contratação

**1. Submissão do Pedido e Injeção de Contexto**: O fluxo é iniciado pelo tutor após a escolha de um cuidador específico nos resultados de busca. O tutor seleciona as datas desejadas no calendário e o software anexa automaticamente o perfil completo do animal à solicitação. O estado da transação no banco de dados é inicializado como `CRIADA`.

**2. Bloqueio Financeiro Preventivo**
Para evitar que o tutor dispare solicitações simultâneas para dezenas de cuidadores, o sistema exige a validação financeira imediata. O tutor insere os dados do cartão de crédito, e o backend da plataforma comunica-se com a API do gateway de pagamento enviando um comando de pré-autorização (_Pre-Auth_). O gateway reserva o limite correspondente ao valor total do serviço na fatura do tutor, garantindo que os fundos existem, mas não efetua a liquidação financeira. A transação transita para o estado `PENDENTE`.

**3. Janela de Análise** 
O cuidador recebe uma notificação informando sobre a nova solicitação.

Neste momento, o servidor aciona um temporizador estabelecendo um tempo máximo de resposta que o cuidador possui para interagir com o pedido. No mercado pet, esse SLA geralmente é fixado entre 12 e 24 horas. Durante essa janela temporal, as datas solicitadas sofrem um bloqueio provisório no calendário do cuidador, impedindo que outros tutores enviem solicitações diretas para os mesmos dias.

**4. Avaliação de Compatibilidade e Comunicação (Meet & Greet)**

Antes de clicar no botão de confirmação, o cuidador utiliza o chat interno do aplicativo para fazer perguntas adicionais ao tutor sobre o comportamento do animal.

Plataformas como a Rover possuem funcionalidades de interface que incentivam o agendamento de um encontro presencial prévio (_Meet & Greet_) para que o cuidador avalie a agressividade ou ansiedade do pet. O sistema mantém o estado da reserva inalterado (`PENDENTE`) durante toda a troca de mensagens, desde que o prazo do SLA não seja estourado.

  

### 5. Resolução da Transação (Gatilhos de Fechamento)

O fim do processo assíncrono ocorre por meio de três possíveis gatilhos, cada um gerando uma resposta arquitetural diferente no software:

  

- **Cenário A: Aceite Manual (Confirmação):** O cuidador clica em "Aceitar". O backend dispara um comando de captura (_Capture_) para a API de pagamentos, transformando a pré-autorização em uma cobrança real e irreversível. O valor entra na subconta de custódia da plataforma. A transação muda para o estado `CONFIRMADA` e o bloqueio no calendário do cuidador torna-se definitivo.
    
      
    
- **Cenário B: Recusa Direta:** O cuidador avalia que o animal não é compatível com o seu ambiente e clica em "Recusar". O servidor envia um comando de cancelamento (_Void_) para o gateway de pagamento. O limite do cartão do tutor é restaurado instantaneamente, a transação passa para o estado `RECUSADA` e o calendário do cuidador é liberado imediatamente.
    
      
    
- **Cenário C: Expiração por Tempo (Timeout):** O cuidador não interage com o aplicativo até o fim do contador do SLA. O sistema processa automaticamente o evento de _Timeout_. O comando de _Void_ é acionado no cartão do tutor, e a reserva recebe o status `EXPIRADA`. Como consequência lógica, o algoritmo de recomendação da plataforma penaliza o cuidador, rebaixando temporariamente a sua posição nas listagens de busca como sanção pela falta de responsividade.