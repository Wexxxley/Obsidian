

---
- 3 papeis: tutor, cuidador, admin.
- App mobile para tutor e cuidador.
- Somente API para o admin.
### Gestão de Contas e Perfis 
- **US01:** Como Tutor, eu quero realizar o cadastro utilizando e-mail e senha, para que eu possa acessar a plataforma rapidamente e visualizar os serviços disponíveis.
	- **US02.1:** Como Cuidador, eu quero fornecer o meu número de CPF válido, endereço e documentação básica durante a etapa de cadastro, para que o sistema registre minha identidade legal de forma unívoca no banco de dados.
	- **US02.2:** Como Cuidador, eu quero capturar uma fotografia facial em tempo real utilizando estritamente a câmera nativa do aplicativo, para que o sistema impeça o _upload_ de imagens da galeria e evite fraudes de identidade.
	- **US02.3:** Como Cuidador, eu quero conceder o aceite legal no aplicativo autorizando a consulta de verificação de antecedentes criminais atrelada ao meu CPF, para que a plataforma cumpra os requisitos de segurança exigidos pelos tutores.
	- **US02.4:** Como Cuidador, eu quero anexar as fotografias dos ambientes delimitados da minha residência ainda na esteira de cadastro inicial, para enviar a comprovação visual de que possuo um espaço seguro para a hospedagem.
	- **US02.5:** Como Cuidador, eu quero visualizar uma tela com o status bloqueado "Cadastro em Análise" imediatamente após concluir o envio de todos os arquivos, para compreender que a liberação da conta ocorre de forma assíncrona e depende de uma verificação humana.
	- **US02.6:** Como Administrador, eu quero consumir um endpoint na API que retorne a fila de requisições pendentes contendo as informações de cadastro dos cuidadore (checagem criminal) para realizar a auditoria de segurança documental.
	- **US02.7:** Como Administrador, eu quero executar o comando de "Aprovar" ou "Rejeitar (DEFINITIVAMENTE ou não)" (no caso de rejeitar com um feedback) na ficha do cuidador através da API, para que a máquina de estados do banco de dados altere a permissão daquele usuário e dispare uma notificação automática informando a decisão final.
- **US03:** Como Tutor, eu quero cadastrar múltiplos perfis de pets informando espécie, porte, raça, e dados médicos (==TENHO QUE ESPECIFICAR AINDA==) para que o cuidador saiba exatamente quem será hospedado.
- **US04**: Como Tutor, eu quero preencher um questionário de compatibilidade (reação a outros animais, crianças e barulhos), para que o sistema cruze essas informações com o ambiente do cuidador e evite agendamentos de alto risco.
- **US05:** Como Tutor, eu quero informar o meu veterinário de confiança, para que o cuidador tenha respaldo médico em emergências.
- **US06:** Como Cuidador, eu quero configurar minha faixa de disponibilidade diária  para que eu alinhe as expectativas do tutor sem expor minha rotina pessoal ou profissional.
    - "Tempo Integral em Casa", "Ausências Curtas (Até 4 horas)" ou "Ausências Longas (Horário Comercial, mais de 6 horas)".
- **US07:** Como Cuidador, eu quero enviar fotos restritas apenas aos ambientes onde o animal circulará (quartos, quintal delimitado), para que eu comprove minha infraestrutura sem expor a privacidade do restante da minha residência.
- **US08:** Como Cuidador, eu quero configurar quais portes/espécies dou preferência.
- **US09:** Como Cuidador, eu quero marcar no meu perfil se ofereço o serviço adicional de transporte (busca e entrega), para que eu possa monetizar essa facilidade logística.

---
### 2. Descoberta, Demanda e Negociação
- **US010:** Como Tutor, eu quero publicar uma demanda informando as datas, o pet e minhas exigências, para que múltiplos cuidadores possam visualizar e enviar propostas.
- **US11:** Como Cuidador, eu quero visualizar um feed de demandas filtrado pela minha capacidade e região, para que eu possa enviar uma proposta para hospedar o animal.
- **US12:** Como Tutor, eu quero buscar cuidadores específicos utilizando filtros de distância, preço e especialidade, para enviar uma proposta direta de hospedagem de forma privada.
- **US13:** Como Cuidador, eu quero receber notificações quando uma proposta direta for enviada para mim, para que eu possa aceitar ou recusar rapidamente antes do tempo limite expirar.
- **US14:** Como Tutor e Cuidador, eu quero ter acesso a um chat temporário antes do pagamento da reserva, para que possamos alinhar rotinas, tirar dúvidas e fechar detalhes do transporte.    
- **US15:** Como Cuidador, eu quero acessar o perfil completo do pet e do cuidador antes de enviar um lance no feed ou aceitar um pedido direto.
- **US16:** Como Cuidador, eu quero poder enviar uma contraproposta financeira, para viabilizar a negociação caso o período exija um esforço maior (como feriados ou necessidades médicas específicas do pet).
- **US22:** Como Cuidador, eu quero ter a capacidade de cancelar um lance financeiro que enviei caso o tutor não responda em tempo hábil e a minha agenda seja preenchida por outro serviço.
### Ciclo de Vida e Contingências da Negociação
    
    
- **US23:** Como Cuidador, eu quero que o feed de demandas públicas atualize dinamicamente, removendo automaticamente as vagas que já foram preenchidas por outros cuidadores ou canceladas pelos tutores, garantindo que eu invista tempo analisando apenas oportunidades reais.
### Épico 3: Contratação
- **US14:** Como Tutor, eu quero parametrizar a frequência diária de envio do "Diário de Estadia" (ex: a cada 3 horas, ou apenas nas refeições) no momento da contratação, para que minhas expectativas de comunicação fiquem alinhadas contratualmente.
- **US15:** Como Tutor, eu quero estipular um limite financeiro pré-aprovado para gastos emergenciais (Teto de Gastos) no momento do pagamento, para que o cuidador saiba até onde pode agir sem minha autorização explícita.
    
      
    
- **US16:** Como Tutor, eu quero efetuar o pagamento integral via cartão de crédito ou Pix diretamente no aplicativo, para que a transação fique protegida pela plataforma até o fim do serviço.
    
      
    
- **US17:** Como Cuidador, eu quero ter a garantia de que o dinheiro do tutor está retido sob custódia da plataforma (Escrow) no momento em que a reserva muda para o status de confirmada, para que eu não sofra calotes ao fim da estadia.
    
      
    
- **US18:** Como Tutor e Cuidador, eu quero visualizar e aceitar o Termo de Responsabilidade gerado dinamicamente com os dados exatos da hospedagem (datas, valores, teto de emergência), para ter respaldo legal da prestação de serviço.
    
      
    

### Épico 4: Execução, Auditoria e Emergências

Este épico mapeia o ciclo de vida do pet dentro da casa do cuidador, garantindo mecanismos de defesa contra litígios.

  

- **US19:** Como Cuidador, eu quero registrar o check-in do pet utilizando exclusivamente a câmera nativa do aplicativo (sem acesso à galeria), para que o sistema extraia a data e hora exatas (Metadados EXIF) e eu tenha provas do estado físico do animal ao chegar.
    
      
    
- **US20:** Como Tutor, eu quero receber uma notificação automática assim que o check-in fotográfico for concluído, para ter a confirmação do início seguro da estadia.
    
      
    
- **US21:** Como Cuidador, eu quero receber lembretes do aplicativo baseados na frequência parametrizada pelo tutor, para que eu não esqueça de enviar as fotos e vídeos obrigatórios da alimentação e higiene.
    
      
    
- **US22:** Como Cuidador, eu quero possuir um botão de "Alerta Crítico de Saúde", para que eu possa emitir um aviso que sobreponha o modo silencioso do celular do tutor caso o animal sofra um acidente grave.
    
      
    
- **US23:** Como Cuidador, eu quero poder enviar os recibos de clínicas veterinárias através do sistema caso o tutor fique incomunicável, para que a plataforma registre o uso daquele "Teto de Gastos" pré-aprovado.
    
      
    

### Épico 5: Encerramento, Multas e Estornos

O foco aqui é a finalização do ciclo, o repasse financeiro e as regras de cancelamento.

  

- **US24:** Como Cuidador, eu quero registrar o check-out do pet novamente com a câmera nativa do sistema, para comprovar que devolvi o animal sem novos ferimentos.
    
      
    
- **US25:** Como Tutor, caso eu precise cancelar a hospedagem antes do início, eu quero que o sistema calcule meu reembolso automaticamente com base nas regras de proximidade da data, para que eu receba o estorno sem precisar acionar o suporte.
    
      
    
- **US26:** Como Tutor, caso eu decida buscar o animal dias ou horas antes do término contratado, eu quero que o sistema realize o recálculo e o estorno proporcional das horas não utilizadas, para que eu pague apenas pelo tempo efetivo.
    
      
    
- **US27:** Como Cuidador, caso o tutor atrase severamente a busca do animal (além do período de tolerância), eu quero que o sistema cobre automaticamente diárias adicionais no cartão de crédito do tutor, para que meu tempo extra seja remunerado.
    
      
    
- **US28:** Como Cuidador, eu quero que o meu repasse financeiro, subtraído da taxa da plataforma, seja liberado automaticamente para minha conta bancária ou Pix cadastrado logo após a validação do check-out.
    
      
    

### Épico 6: Sistema Tridirecional de Avaliações

O mecanismo de reputação é essencial para manter a qualidade da rede.

  

- **US29:** Como Tutor, eu quero avaliar o serviço do cuidador de 1 a 5 estrelas e deixar um comentário público, para auxiliar outros usuários na tomada de decisão.
    
      
    
- **US30:** Como Cuidador, eu quero avaliar o tutor em relação à pontualidade e comunicação, para que outros prestadores de serviço saibam se aquele cliente é problemático.
    
      
    
- **US31:** Como Cuidador, eu quero registrar um laudo comportamental do pet (ex: destruiu móveis, chorou muito, foi dócil), que ficará oculto para os tutores, mas visível para outros cuidadores, para que a comunidade se proteja contra animais difíceis.
    
      
    

### Épico 7: Administração do Sistema (API)

Requisitos técnicos estruturais executados nos bastidores para gerenciar o ecossistema.

  

- **US32:** Como Administrador, eu quero consumir um endpoint na API para aprovar ou rejeitar a documentação enviada por um novo cuidador, para que ele possa começar a receber solicitações.
    
      
    
- **US33:** Como Administrador, eu quero ter autonomia técnica via API para bloquear contas de tutores ou cuidadores que violem os termos de uso, impedindo novos logins.
    
      
    
- **US34:** Como Administrador, eu quero possuir uma rota na API para forçar o estorno manual de uma transação diretamente no gateway de pagamento, para resolver casos de litígio onde a automação do sistema não seja aplicável.
    
      
    
- **US35:** Como Administrador, eu quero alterar as variáveis globais de taxa de comissão e tempo de tolerância de atrasos diretamente no banco de dados, para que a plataforma se adapte a novas estratégias comerciais sem exigir atualização nos aplicativos.