

---

Para tutores: Mãe, ster, alice, yasmin, liniker, maurilio
Para cuidadores: Avelino, eduardo, grazy, junior.

---
## 1. Com tutores

"Olá! Meu nome é Wesley, sou estudante do curso de Ciência da Computação e esta entrevista faz parte da etapa de pesquisa para o meu Trabalho de Conclusão de Curso. Estou desenvolvendo a arquitetura e os requisitos técnicos de uma plataforma chamada Mimo, idealizado para conectar tutores de pets a cuidadores locais. O objetivo do sistema é modernizar e trazer segurança para o processo de hospedagem de animais.

O objetivo dessa conversa é entender as suas reais necessidades, preocupações e expectativas de monitoramento ao deixar o seu animal com terceiros. As suas respostas serão utilizadas para fins acadêmicos, servindo como base para definir as funcionalidades do aplicativo."
### 1.1 Contextualização do Cenário Atual

- Quando você precisa se ausentar e não pode levar o seu pet, qual é a alternativa que você mais utiliza atualmente?
    
- Como você descreveria o perfil do seu animal em relação à sociabilidade com pessoas estranhas, interação com outros animais e nível de energia? 

- Quais barreiras você teria para contratar esse tipo de serviço?
### 1.2 Coleta de Dados Clínicos e Preventivos

- Existe alguma restrição comportamental do seu pet ou algum problema de saúde  que o sistema deve exibir como um alerta antes que um cuidador aceite a reserva?
    
- O seu pet faz uso de alguma medicação de uso contínuo? Se sim, você consideraria útil que o sistema possuísse uma funcionalidade de "Alarme de Medicação" para notificar o cuidador nos horários exatos definidos por você?
    - Parra o match entre pet e cuidador.
    
- Quais itens pertencentes ao pet geralmente precisam acompanhá-lo? (como ração, brinquedos, caminha) 
### 1.3 Fluxos de Emergência Médica

- Em um cenário hipotético onde seu pet apresenta um problema de saúde durante a hospedagem, como você gostaria de ser notificado? (alerta no app, SMS, ligação)
    
- Se a notificação inicial não for respondida? O sistema deve orientar o cuidador a levar o animal exclusivamente à clínica veterinária previamente cadastrada no perfil do pet, ou autorizar o deslocamento para a clínicamais próxima?

- O aplicativo deve exigir que o cuidador registre fotos ou vídeos curtos do animal apresentando os sintomas físicos antes de autorizar formalmente a ida ao veterinário?

- Em caso de doença natural, se o cuidador levar o pet ao veterinário e custear com o próprio bolso, você teria problema em reembolsá-lo? Você gostaria de estabelecer um "Teto de Gastos Pré-Aprovado" para emergências?
### 1.4 Gestão de Riscos Críticos 

- Para que você se sinta resguardado juridicamente em caso de negligência ou maus-tratos, quais evidências você espera que o aplicativo armazene durante a estadia (exemplo: fotos, marcação exata de horário e localização no aplicativo)?
### 1.4 Diário de Estadia e Expectativas de Monitoramento

- Durante o período em que estiver ausente, com qual frequência diária mínima você exige que o cuidador alimente o sistema com fotos, vídeos?

- Caso contrate o serviço, você teria preferência por entregar o pet presencialmente na residência do cuidador para avaliar o ambiente, ou a plataforma deve permitir a negociação de uma taxa extra de transporte para o cuidador buscar o animal na sua residência?

- Você estaria disposto a assumir a responsabilidade exclusiva pelo fornecimento de toda a alimentação durante o período, ou acredita que o aplicativo deveria permitir a inclusão do custo da ração na taxa da diária cobrada pelo cuidador?

- Você concorda que o sistema deve reter o pagamento ao cuidador até que você acesse o aplicativo e confirme o recebimento do pet em perfeitas condições?
	- Recomendação: o cuidador deve lembrá-lo disso.

- Quais características o sistema precisa exibir no perfil de um cuidador para que você sinta confiança suficiente para iniciar uma reserva? (avaliações, fotos do ambiente)

- Quais mecanismos (fora os falados até então) você acha que a plataforma deve ter para passar máxima confiança?

---
## 2. Com cuidadores

"Olá! Meu nome é Wesley, sou estudante de Ciência da Computação e estou conduzindo esta entrevista como parte do levantamento de dados para o meu Trabalho de Conclusão de Curso. Estou desenvolvendo a arquitetura e os requisitos técnicos de uma plataforma chamada Mimo, idealizado para conectar tutores de pets a cuidadores locais. O objetivo do sistema é modernizar e trazer segurança para o processo de hospedagem de animais.

O objetivo desta conversa é explorar um cenário hipotético: caso o aplicativo estivesse funcionando hoje e você decidisse se cadastrar para hospedar o animal de uma pessoa desconhecida, quais seriam as suas principais exigências, preocupações e limites operacionais para aceitar esse trabalho de forma segura? As informações que você compartilhar me ajudarão a definir os requisitos técnicos do aplicativo."
### 2.1 Contextualização e Limites Operacionais

- Para que você pudesse realizar a hospedagem, quais restrições físicas ou de rotina você precisaria configurar no seu perfil? (limite de tamanho do animal, se aceita apenas cães ou gatos).
    
- Você consideraria viável hospedar animais de tutores diferentes no mesmo período? Se sim, qual seria seu limite?
    
- Quais informações sobre o comportamento do animal você exigiria que o sistema mostrasse obrigatoriamente antes de você clicar em "Aceitar Reserva"?

### 2.2 Gestão de Riscos Críticos e Segurança do Cuidador

O foco aqui é eliciar as regras de contingência e os Requisitos Não Funcionais de segurança da informação, definindo como o Backoffice (painel administrativo) deve intervir para proteger o cuidador de perdas materiais ou acusações injustas.

- Em um cenário onde o animal causa danos materiais à sua residência, qual mecanismo de proteção você espera que a plataforma ofereça? (Exemplo: um seguro embutido na taxa, a retenção de um valor caução no cartão do tutor, ou um canal direto para mediação legal).
    
- Para se resguardar de acusações de maus-tratos ou fuga por parte do tutor, quais ferramentas de registro você gostaria que o aplicativo gerasse como prova a seu favor? (Exemplo: registro de conversas bloqueado para exclusão, envio de fotos com horário e localização rastreados via GPS do próprio sistema).
    
- Você exigiria que o sistema realizasse alguma verificação de segurança sobre o tutor (como validação de documentos ou checagem de antecedentes criminais) antes de permitir que ele entrasse na sua residência para deixar o animal?
    

### 2.3 Fluxos de Emergência Médica e Suporte Técnico

Este bloco levanta os requisitos da Máquina de Estados (mudança de status da transação) voltados para intercorrências de saúde e as rotinas de comunicação de alta prioridade.

- Caso o animal apresente um mal-estar súbito e você não consiga contato imediato com o tutor através do aplicativo, qual fluxo de ação o sistema deve liberar para você? (Acionamento de um suporte veterinário online da própria plataforma, ou o deslocamento para a clínica cadastrada no perfil do animal).
    
- Se for necessário levar o pet a uma emergência veterinária física e o aplicativo recomendar que você pague a consulta para posterior reembolso, qual seria o seu nível de resistência a essa regra? Você exigiria que a plataforma transferisse um valor emergencial imediato para a sua conta antes do atendimento?
    
- Qual seria o canal de suporte da plataforma (chat interno, botão de SOS, telefone 24h) que traria mais tranquilidade para você reportar uma emergência?
    

### 2.4 Diário de Estadia e Integração Logística

O objetivo é extrair os parâmetros de usabilidade do aplicativo, medindo o quanto o "Diário de Estadia" pode exigir do usuário sem se tornar uma ferramenta burocrática e exaustiva.

- O aplicativo exigirá o envio de fotos e vídeos para manter o tutor informado (o "Diário de Estadia"). Considerando a sua rotina diária, qual seria a frequência máxima de envios obrigatórios por dia que você conseguiria cumprir sem achar o aplicativo invasivo ou cansativo?
    
- Como você gostaria de realizar a contagem do tempo de hospedagem para a cobrança da diária? O sistema deve registrar o horário exato da entrega e da retirada através da leitura de um QR Code, ou um check-in manual via botão no aplicativo já seria suficiente?
    
- Você estaria disposto a oferecer, como um serviço extra cobrado pelo aplicativo, a busca e entrega do animal na casa do tutor?
    

### 2.5 Pagamentos e Formalização Legal

Esta etapa visa definir a aceitação do modelo de Custódia (Escrow) e as regras de aceite do Contrato de Depósito, determinando o fluxo do módulo financeiro.

- Você teria algum problema em aceitar a responsabilidade legal temporária sobre o animal (assinando um termo digital de aceite) em casos de incidentes ocorridos por descuido na sua residência, desde que as doenças preexistentes fossem isentas?
    
- Sobre o fluxo financeiro: a plataforma receberá o pagamento do tutor no ato da reserva, reterá a taxa de comissão e liberará o seu pagamento apenas após o término da estadia. Esse modelo de retenção para garantir a segurança da transação é aceitável para você?
    
- Qual seria o prazo máximo tolerável, após o tutor buscar o animal, para que o sistema transferisse o dinheiro para a sua conta bancária?