

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
- **US10:** Como Tutor, eu quero publicar um pedido no "Feed de demandas públicas", para que múltiplos cuidadores possam visualizar a minha necessidade e iniciar uma negociação comigo
- **US11:** Como Tutor, eu quero enviar uma "Proposta Direta" de hospedagem para o perfil de um cuidador específico, para que a solicitação chegue de forma privada e exclusiva a ele.
- **US12:** Como Cuidador, eu quero visualizar o "Feed de demandas públicas" para que eu possa analisar as solicitações abertas e acionar a opção de enviar uma mensagem direta aos tutores de meu interesse.
- **US13:** Como Cuidador, ao receber uma "Proposta Direta" de um tutor, eu quero ter a opção de recusar imediatamente o pedido ou abrir um canal de mensagem direta, para que eu possa gerenciar minha agenda e iniciar as tratativas.
- **US14:** Como Tutor e Cuidador, eu quero utilizar um chat interno vinculado à demanda, para que possamos alinhar as necessidades do animal e chegar a um acordo financeiro preliminar através de mensagens.
- **US15:** Como Cuidador, eu quero acionar uma funcionalidade dentro do chat para inserir o valor final negociado e a qtd vezes que me disponibilizo a envia atualizações por dia (mínimo 2), para que o sistema gere e apresente um rascunho do contrato de prestação de serviço contendo os valores e as datas para a análise do tutor.
- **US16:** Como Tutor, ao receber a proposta financeira gerada pelo cuidador, eu quero ter a opção de recusar (devido a erros de digitação do cuidador ou discordância de valores), para que a cobrança seja cancelada, mas o chat permaneça ativo permitindo a continuidade da negociação.
- **US17:** Como Tutor, ao concordar com o valor gerado pelo cuidador, eu quero visualizar e conceder o aceite eletrônico no contrato de prestação de serviço, para que o sistema formalize o acordo e altere o status da demanda para "Aguardando Pagamento".    
- **US18:** Como Tutor, eu quero ser direcionado automaticamente para a tela de pagamento após o aceite do contrato, podendo selecionar o método de transação (Pix ou Cartão de Crédito), para que eu possa efetivar a reserva.
- **US19:** Como Tutor, eu quero estipular um limite financeiro pré-aprovado para gastos emergenciais no momento do pagamento, para que o cuidador saiba até onde pode agir em caso de emergência e eu nao puder ser contatado.
- **US20:** Como Regra de Negócio, a plataforma deve realizar a retenção integral do montante transacionado no momento do pagamento, mantendo o valor sob custódia  até o evento  de finalização do pedido, garantindo assim a segurança do repasse financeiro.
- **US21:** Como Tutor e Cuidador, o contrato gerado dinamicamente com os dados exatos da hospedagem, para ter respaldo legal da prestação de serviço.
![](../../attachments/Pasted%20image%2020260901081032.png)
### Épico 4: Execução, Auditoria e Emergências
- **US22:** Como Cuidador, eu quero registrar o check-in do pet utilizando exclusivamente a câmera nativa do aplicativo (sem acesso à galeria), para que o sistema extraia a data e hora exata e eu tenha provas do estado físico do animal ao chegar.
- **US23:** Como Tutor, eu quero receber uma notificação automática assim que o check-in fotográfico for concluído, para ter a confirmação do início seguro da estadia.
- **US24:** Como Cuidador, eu quero receber lembretes do aplicativo baseados na frequência do contrato, para que eu não esqueça de enviar as fotos e vídeos obrigatórios.
- **US25:** Como Cuidador, eu quero possuir um botão de "Alerta de Saúde", para que eu possa emitir um aviso que sobreponha o modo silencioso do celular do tutor caso o animal sofra um acidente grave.
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