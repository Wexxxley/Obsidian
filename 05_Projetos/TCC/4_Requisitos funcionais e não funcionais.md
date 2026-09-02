
---
- 3 papeis: tutor, cuidador, admin.
- App mobile para tutor e cuidador.
- Somente API para o admin.

Pode ter uma seção "Requisitos Fora de Escopo":
- Backoffice robusto para mediação de litígios.

---
## 1. Requisitos funcionais
### 1. Gestão de Contas e Perfis

- **US01:** Como Tutor, eu quero realizar o cadastro utilizando e-mail e senha (CEP para o cadastro), para que eu possa acessar a plataforma rapidamente e visualizar os serviços disponíveis.
	- **US02:** Como Cuidador, eu quero fornecer o meu número de CPF válido, endereço e documentação básica durante a etapa de cadastro, para que o sistema registre minha identidade legal de forma unívoca no banco de dados.
	- **US03:** Como Cuidador, eu quero capturar uma fotografia facial em tempo real utilizando estritamente a câmera nativa do aplicativo, para que o sistema impeça o upload de imagens da galeria e evite fraudes de identidade.
	- **US04:** Como Cuidador, eu quero conceder o aceite legal no aplicativo autorizando a consulta de verificação de antecedentes criminais atrelada ao meu CPF, para que a plataforma cumpra os requisitos de segurança exigidos pelos tutores.
	- **US05:** Como Cuidador, eu quero anexar as fotografias dos ambientes delimitados da minha residência ainda na esteira de cadastro inicial, para enviar a comprovação visual de que possuo um espaço seguro para a hospedagem.
	- **US06:** Como Cuidador, eu quero visualizar uma tela com o status bloqueado "Cadastro em Análise" imediatamente após concluir o envio de todos os arquivos, para compreender que a liberação da conta ocorre de forma assíncrona e depende de uma verificação humana.
- **US07:** Como Tutor, eu quero cadastrar múltiplos perfis de pets informando espécie, porte, raça, e dados médicos (por meio de perguntas, checkbox, sem ser invasivo) para que o cuidador saiba exatamente quem será hospedado.
- **US08:** Como Tutor, eu quero preencher um questionário de compatibilidade (reação a outros animais, crianças e barulhos), para que o sistema cruze essas informações com o ambiente do cuidador e evite agendamentos de alto risco.
- **US09:** Como Tutor, eu quero informar o meu veterinário de confiança, para que o cuidador tenha respaldo médico em emergências.
- **US10:** Como Cuidador, eu quero configurar minha faixa de disponibilidade diária para que eu alinhe as expectativas do tutor sem expor minha rotina pessoal ou profissional: "Tempo Integral em Casa", "Ausências Curtas (Até 4 horas)" ou "Ausências Longas (Horário Comercial, mais de 6 horas)".
- **US11:** Como Cuidador, eu quero enviar fotos restritas apenas aos ambientes onde o animal circulará (quartos, quintal delimitado), para que eu comprove minha infraestrutura sem expor a privacidade do restante da minha residência.
- **US12:** Como Cuidador, eu quero configurar quais portes/espécies dou preferência.
- **US13:** Como Cuidador, eu quero marcar no meu perfil se ofereço o serviço adicional de transporte (busca e entrega), para que eu possa monetizar essa facilidade logística.
- **US14:** Como Tutor e Cuidador, eu quero ter acesso a uma funcionalidade de suporte (link para o WhatsApp já é suficiente).
- **US15:** Como Cuidador, eu quero cadastrar e validar a minha chave Pix na plataforma, para que o sistema de pagamentos possua um roteamento financeiro exato para transferir a minha remuneração ao término dos serviços.

### 2. Descoberta, Demanda e Negociação

- **US16:** Como Tutor, eu quero publicar um pedido no "Feed de demandas públicas", para que múltiplos cuidadores possam visualizar a minha necessidade e iniciar uma negociação comigo.
- **US17:** Como Tutor, eu quero enviar uma "Proposta Direta" de hospedagem para o perfil de um cuidador específico, para que a solicitação chegue de forma privada e exclusiva a ele
- **US18:** Como Cuidador, eu quero visualizar o "Feed de demandas públicas" para que eu possa analisar as solicitações abertas e acionar a opção de enviar uma mensagem direta aos tutores de meu interesse.
- **US19:** Como Cuidador, ao receber uma "Proposta Direta" de um tutor, eu quero ter a opção de recusar imediatamente o pedido ou abrir um canal de mensagem direta, para que eu possa gerenciar minha agenda e iniciar as tratativas.    
- **US20:** Como Tutor e Cuidador, eu quero utilizar um chat interno vinculado à demanda, para que possamos alinhar as necessidades do animal e chegar a um acordo financeiro preliminar através de mensagens.
- **US21:** Como Cuidador, eu quero acionar uma funcionalidade dentro do chat para inserir o valor final negociado e a quantidade de vezes que me disponibilizo a enviar atualizações por dia (mínimo 2), para que o sistema gere e apresente um rascunho do contrato de prestação de serviço contendo os valores e as datas para a análise do tutor.
- **US22:** Como Tutor, ao receber a proposta financeira gerada pelo cuidador, eu quero ter a opção de recusar (devido a erros de digitação do cuidador ou discordância de valores), para que a cobrança seja cancelada, mas o chat permaneça ativo permitindo a continuidade da negociação.
- **US23:** Como Tutor, ao concordar com o valor gerado pelo cuidador, eu quero visualizar e conceder o aceite eletrônico no contrato de prestação de serviço, para que o sistema formalize o acordo e altere o status da demanda para "Aguardando Pagamento".
- **US24:** Como Tutor, eu quero ser direcionado automaticamente para a tela de pagamento após o aceite do contrato, podendo selecionar o método de transação (Pix ou Cartão de Crédito), para que eu possa efetivar a reserva.
- **US25:** Como Tutor, eu quero estipular um limite financeiro pré-aprovado para gastos emergenciais no momento do pagamento, para que o cuidador saiba até onde pode agir em caso de emergência e eu não puder ser contatado.
- **US26:** Como Tutor e Cuidador, eu quero visualizar o contrato gerado dinamicamente com os dados exatos da hospedagem, para ter respaldo legal da prestação de serviço.

### 3. Execução, Auditoria e Emergências

- **US27:** Como Cuidador, eu quero registrar o check-in do pet utilizando exclusivamente a câmera nativa do aplicativo (sem acesso à galeria), para que o sistema extraia a data e hora exata e eu tenha provas do estado físico do animal ao chegar.
- **US28:** Como Tutor, eu quero receber uma notificação automática assim que o check-in fotográfico for concluído, para ter a confirmação do início seguro da estadia.
- **US29:** Como Cuidador, eu quero receber lembretes do aplicativo baseados na frequência do contrato, para que eu não esqueça de enviar as fotos e vídeos obrigatórios.
- **US30:** Como Cuidador, eu quero possuir um botão de "Alerta de Saúde", para que eu possa emitir um aviso que sobreponha o modo silencioso do celular do tutor caso o animal sofra um acidente grave.
- **US31:** Como Cuidador, eu quero realizar o upload do laudo veterinário e do comprovante fiscal (nota fiscal) diretamente no detalhe da reserva em andamento, para que o sistema registre formalmente o gasto dentro do "Teto de Gastos" pré-aprovado e adicione esse montante como uma pendência financeira obrigatória para o tutor quitar antes de realizar o check-out.

### 4. Encerramento, Multas e Estornos

- **US32:** Como Cuidador, eu quero registrar o check-out do pet novamente com a câmera nativa do sistema, para comprovar que devolvi o animal.
- **US33:** Como Tutor, caso eu precise cancelar a hospedagem antes do início, eu quero que o sistema calcule meu reembolso automaticamente, para que eu receba o estorno sem precisar acionar o suporte.
- **US34:** Como Tutor, caso eu decida buscar o animal dias antes do término contratado, eu quero que o sistema realize o recálculo e o estorno dos dias não utilizados, para que eu pague apenas pelo tempo efetivo.
- **US35:** Como Cuidador, eu quero iniciar a finalização do serviço acionando a funcionalidade de check-out e capturar a fotografia do animal utilizando a câmera nativa.
- **US36:** Como Tutor, ao receber a notificação de que o check-out foi iniciado pelo cuidador, eu quero Confirmar Recebimento no aplicativo.

### 5. Avaliações

- **US37:** Como Tutor, eu quero avaliar o serviço do cuidador de 1 a 5 estrelas e deixar um comentário público, para auxiliar outros usuários na tomada de decisão.
- **US38:** Como Cuidador, eu quero avaliar o tutor em relação à pontualidade e comunicação, para que outros prestadores de serviço saibam se aquele cliente é problemático. A nota do tutor é visível por todos. A nota com comentário só pelos cuidadores.
- **US39:** Como Cuidador, eu quero dar uma avaliação para o pet (ex: destruiu móveis, chorou muito, foi dócil), que ficará oculta para os tutores, mas visível para outros cuidadores, para que a comunidade se proteja contra animais difíceis.

### 6. Administração do Sistema

- **US40:** Como Administrador, eu quero consumir um endpoint na API que retorne a fila de requisições pendentes de novos cuidadores.
- **US41:** Como Administrador, eu quero executar o comando de "Aprovar" ou "Rejeitar" na ficha do cuidador através da API. Em caso de rejeição por falha simples, o sistema deve registrar o motivo (feedback) e manter a conta aberta para correção. Em caso de violação grave, o sistema deve adicionar o CPF a uma Lista de Bloqueio.

---
## 2. Requisitos não funcionais

- **RN01 - Retenção de Custódia:** A plataforma deve realizar a retenção integral do montante transacionado no momento do pagamento, mantendo o valor sob custódia até o evento de finalização do pedido, garantindo assim a segurança do repasse financeiro.
- **RN02 - Aceite Tácito:** Se o tutor negligencia a confirmação no aplicativo, após 10 horas o sistema aplica o princípio de Aceite Tácito.
- **RN03 - Armazenamento Temporário:** O aplicativo deve reter os dados de Check-in e Check-out em armazenamento temporário (Cache Local) caso o meu celular esteja sem sinal de internet no momento da entrega do animal, realizando o envio das provas fotográficas para o servidor automaticamente assim que a conexão for restabelecida.
- **RN04 - Timeout de Proposta Direta:** Uma proposta direta de hospedagem enviada por um tutor que não receba aceite ou recusa por parte do cuidador deve expirar sistematicamente em exatamente 6 horas.
- **RNF05 - Autenticação Stateless :** A comunicação entre o aplicativo móvel (frontend) e a API (backend) deve operar por meio de autenticação baseada em JWT (_JSON Web Tokens_). A API não deve manter sessões ativas na memória do servidor, exigindo que cada requisição do aplicativo envie o token criptografado no cabeçalho para validar a identidade.
- **RNF07 - Comunicação chat:** Para reduzir a carga de processamento do servidor em .NET e simplificar a arquitetura, o fluxo de mensagens em tempo real do chat não utilizará WebSockets gerenciados pela sua API (como o SignalR). O aplicativo móvel deve assinar diretamente o módulo de _Realtime_ do Supabase para receber as atualizações instantâneas de novas mensagens.
    
- **RNF07 - Gestão de Estados em Tempo de Execução:** A arquitetura do sistema não deve depender de tarefas automatizadas em segundo plano (_Cron Jobs_ ou _Worker Services_) para alterar status de entidades com base no tempo. As expirações (como o tempo limite de uma Proposta Direta ou o bloqueio de um chat inativo) devem ser calculadas de forma dinâmica através de funções matemáticas pela API no momento exato em que a requisição de leitura for realizada.
    

**Disponibilidade e Tolerância a Falhas**

- **RNF08 - Armazenamento Temporário (Cache Local):** O aplicativo móvel deve possuir capacidade de resiliência a quedas de rede durante operações críticas de segurança. Se o dispositivo do cuidador perder a conexão de internet no momento da captura fotográfica do check-in ou do check-out, a aplicação deve gravar a foto e seus respectivos metadados no armazenamento criptografado do celular e tentar retransmitir a carga útil de forma invisível ao usuário assim que o sistema operacional reportar o restabelecimento da conectividade.
    

**Compatibilidade**

- **RNF09 - Nível Mínimo do Sistema Operacional:** O aplicativo móvel desenvolvido em Jetpack Compose deve estabelecer uma versão mínima de sistema operacional (como Android 8.0 / API Level 26) para garantir suporte adequado e estável às bibliotecas modernas de controle de câmera nativa, criptografia em hardware e consumo de APIs assíncronas.