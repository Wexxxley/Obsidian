

---

### **1. Pagamento com Retenção em Custódia**

- **Estados da Transação:** O banco de dados precisará gerenciar um ciclo de vida para os pedidos (ex: `CRIADO`, `PAGO_RETIDO`, `EM_ANDAMENTO`, `CONCLUIDO_LIBERADO`, `ESTORNADO`).
    
- A plataforma deve implementar endpoints para escutar eventos assíncronos enviados pelo gateway (confirmação de pagamento, falhas de repasse, etc), garantindo que o status no banco de dados esteja sincronizado.
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
### 6. Fluxo de Contratação

**A Interface do Tutor**: O sistema deve oferecer fluxos distintos para a contratação do serviço de hospedagem.

- **Opção A - Demanda Geral:** O tutor cria um "Card de Demanda" preenchendo um formulário estruturado. Ele informa o período exato (data e hora de entrega/retirada), o perfil detalhado do animal (espécie, porte, nível de energia, sociabilidade) e necessidades específicas (medicação, restrições alimentares). Opcionalmente, pode sugerir um valor base que está disposto a pagar. Este card é publicado em um feed público. Múltiplos cuidadores visualizam a vaga e enviam propostas (lances) com seus respectivos preços. O painel do tutor permite comparar os lances, analisar os perfis dos interessados e aceitar a oferta mais adequada.
    
- **Opção B - Busca Ativa e Proposta Específica:** O tutor acessa um catálogo ou lista de busca para explorar proativamente os perfis dos cuidadores disponíveis na plataforma. O usuário utiliza filtros (como proximidade, tipo de animal aceito ou nota de avaliação) para encontrar um cuidador específico. Ao acessar o perfil desejado, o tutor clica em enviar uma "Proposta Direta". Esta solicitação é enviada de forma privada e exclusiva para aquele cuidador, que pode aceitar, recusar ou negociar o valor.
    
**A Interface do Cuidador**
- **Feed de Vagas Públicas:** A interface principal exibe os Cards de Demanda publicados pelos tutores. O cuidador utiliza filtros para visualizar apenas vagas compatíveis com seu perfil e envia suas ofertas de preço.
- **Caixa de Propostas Diretas:** Área dedicada para solicitações privadas. O cuidador recebe uma notificação isolada, analisa os dados do pet e do período, e responde.
- **Notificação:** O aplicativo utiliza notificações ativas (push notifications) para manter o cuidador engajado frente a novas oportunidades compatíveis.
- **Perfil do Cuidador:** Página que funciona como portfólio. Exibe foto validada, métricas de confiabilidade (nota média e número de serviços concluídos), tipos de animais que aceita, fotos do ambiente e avaliações em texto.
    

---

**7 . Dependencias e possíveis reusos**

- SignalR pode ajudar a criar o chat (existem kits de design já prontos)


**Gateway de Pagamento e Split Financeiro**
Para implementar o modelo de custódia (Escrow) e reter a taxa da plataforma (Take Rate) sem ferir as regulamentações bancárias, o sistema não pode processar ou armazenar dados de cartão de crédito no próprio banco de dados (o que exigiria certificação PCI Compliance). A solução é integrar um provedor financeiro que gerencie contas digitais vinculadas aos cuidadores.
- **Stripe Connect:** É o padrão global para arquiteturas de _Marketplace_. Ele fornece bibliotecas prontas em .NET para realizar requisições de pagamento, pré-autorização e estornos. O sistema permite configurar a regra exata de divisão de valores (Split), enviando a comissão para a conta principal da plataforma e retendo o valor sob custódia na subconta do cuidador.
- **Pagar.me ou Mercado Pago:** São opções com documentação extensa focada no mercado brasileiro, oferecendo integrações nativas e facilitadas para transações via Pix com repasse financeiro automatizado.
      
**Armazenamento de Arquivos em Nuvem (Object Storage)**
O aplicativo exigirá o armazenamento de fotos de perfil dos usuários, fotos dos animais e os arquivos de mídia gerados no "Diário de Estadia". Salvar esses arquivos diretamente em um banco de dados relacional (como strings Base64) degrada o desempenho do sistema e encarece a hospedagem. O padrão arquitetural é enviar o arquivo para um servidor de objetos e salvar apenas a URL pública no seu banco de dados.
- **Cloudinary:** É uma plataforma de gerenciamento de mídia que entrega uma API gratuita muito generosa. Além do armazenamento, ele realiza transformações de imagem em tempo real via URL (como cortar, comprimir e redimensionar imagens pesadas enviadas pelos cuidadores para não travar a interface web).

**Serviços de Geolocalização**
Geolocalização Baseada em Listagem (Sem Mapa Visual). Nesta arquitetura, o tutor informa o seu CEP ou permite que o navegador capture a sua localização atual. O sistema traduz essa posição em coordenadas e a sua API em .NET utiliza a "Fórmula de Haversine". A interface web, então, exibe apenas uma lista tradicional de cuidadores ordenados pelo critério de proximidade, exibindo um texto simples, como "A 2,5 km de distância".
- **ViaCEP:** Uma API pública e gratuita estruturada para buscar endereços no Brasil utilizando o CEP. Permite o preenchimento automático do formulário de cadastro, melhorando a experiência do usuário web.
    
**Bibliotecas Visuais (UI Component Libraries)**
Para a construção do frontend web, desenvolver botões, modais, calendários de seleção de datas e formulários do zero consumiria meses de trabalho. O reuso de código visual acelera a entrega do protótipo e garante uma interface limpa.
- Shadcn-vue 

**Sistemas de Mensageria e Notificação (Push)**
Como detalhado anteriormente, o envio de notificações em segundo plano para a versão web demanda serviços de intermediação entre o seu servidor e o navegador do usuário.

- **Firebase Cloud Messaging (FCM):** O serviço padrão da indústria para o disparo de alertas em tempo real. O servidor .NET envia o comando contendo o texto da notificação para a API do FCM, e o Google se encarrega de rotear e entregar esse alerta visual ao navegador do cuidador, operando de forma totalmente gratuita.