
---

### 1. O Problema

Donos de pets enfrentam barreiras ao precisarem viajar ou se ausentar de suas residências. Em cidades com alto fluxo de estudantes e/ou profissionais que se deslocam entre municípios, como Quixadá, o problema é acentuado.

### 2. A Proposta

A proposta consiste em um Marketplace de Cuidado, uma plataforma que conecta tutores a cuidadores locais. A solução utiliza tecnologia para garantir que o ambiente de estadia seja doméstico e adequado ao perfil específico do animal.

### 3. Fluxo de Contratação (Pré-Serviço)

A ideia é seguir o modelo Marketplace Orientado à Demanda.

**A Interface do Tutor**

Na tela principal do tutor, o sistema deve oferecer fluxos distintos para a contratação do serviço de hospedagem.

- **Opção A - Demanda Geral (Mural Aberto):** O tutor cria um "Card de Demanda" preenchendo um formulário estruturado. Ele informa o período exato (data e hora de entrega/retirada), o perfil detalhado do animal (espécie, porte, nível de energia, sociabilidade) e necessidades específicas (medicação, restrições alimentares). Opcionalmente, pode sugerir um valor base que está disposto a pagar. Este card é publicado em um feed público. Múltiplos cuidadores visualizam a vaga e enviam propostas (lances) com seus respectivos preços. O painel do tutor permite comparar os lances, analisar os perfis dos interessados e aceitar a oferta mais adequada.
    
- **Opção B - Busca Ativa e Proposta Específica:** O tutor acessa um catálogo ou lista de busca para explorar proativamente os perfis dos cuidadores disponíveis na plataforma. O usuário utiliza filtros (como proximidade, tipo de animal aceito ou nota de avaliação) para encontrar um cuidador específico. Ao acessar o perfil desejado, o tutor clica em enviar uma "Proposta Direta". Esta solicitação é enviada de forma privada e exclusiva para aquele cuidador, que pode aceitar, recusar ou negociar o valor.
    

**A Interface do Cuidador**

- **Feed de Vagas Públicas:** A interface principal exibe os Cards de Demanda publicados pelos tutores. O cuidador utiliza filtros para visualizar apenas vagas compatíveis com seu perfil e envia suas ofertas de preço.
    
- **Caixa de Propostas Diretas:** Área dedicada para solicitações privadas. O cuidador recebe uma notificação isolada, analisa os dados do pet e do período, e responde.
    
- **Notificação:** O aplicativo utiliza notificações ativas (push notifications) para manter o cuidador engajado frente a novas oportunidades compatíveis.
    
- **Perfil do Cuidador:** Página que funciona como portfólio. Exibe foto validada, métricas de confiabilidade (nota média e número de serviços concluídos), tipos de animais que aceita, fotos do ambiente e avaliações em texto.
    

### 4. Execução e Acompanhamento (Durante o Serviço)

Esta fase inicia imediatamente após o tutor aceitar a proposta do cuidador e realizar a confirmação na plataforma.

**Abertura do Canal de Comunicação Direta (Chat Interno)**

- **Gatilho de Liberação:** Para evitar que os usuários negociem fora do aplicativo (bypass da plataforma), o chat direto entre tutor e cuidador só deve ser desbloqueado após o "Aceite da Proposta" ou a "Confirmação do Pagamento".
    
- **Funcionalidade:** O chat servirá para o alinhamento de detalhes finais (como endereço exato da residência, envio da localização em tempo real na hora de deixar o animal e orientações de última hora). Ele permanece ativo durante todo o período da estadia, centralizando a comunicação para fins de segurança e auditoria, caso haja algum problema.
    

**Sistema de Relatório Fotográfico Obrigatório**

- **Mecânica de Exigência (SLA de Atualização):** O sistema estabelece um Acordo de Nível de Serviço (SLA) para as atualizações visuais. O cuidador tem a obrigação de enviar uma quantidade $X$ de fotos diárias dentro de janelas de horários pré-estabelecidas (por exemplo: 1 foto entre 08h-10h, 1 foto entre 14h-16h e 1 foto entre 19h-21h).
    
- **Interface do Cuidador (Tarefas Ativas):** Durante o período da hospedagem, a tela inicial do cuidador exibe um painel de "Tarefas Pendentes". O aplicativo envia notificações push alertando: "Faltam 30 minutos para o prazo final do envio da foto da manhã do pet [Nome do Pet]".
    
- **Interface do Tutor (Diário da Estadia):** O tutor recebe acesso a uma tela de acompanhamento contínuo. Nela, as fotos enviadas pelo cuidador aparecem em uma linha do tempo (timeline). O sistema também exibe indicadores de conformidade, mostrando de forma visual (por exemplo, ícones de verificação) que o cuidador está cumprindo os prazos estipulados de envio de imagens, gerando tranquilidade passiva ao tutor.
    

Como você planeja lidar no nível do sistema caso o cuidador descumpra as janelas de horário do envio dessas fotos obrigatórias? O aplicativo aplicará alguma penalidade automática na avaliação dele ou apenas emitirá um alerta ao tutor?

### 5. Rentabilidade

- Comissão por Transação (Take Rate): A principal fonte de receita da plataforma é a cobrança de uma comissão sobre os serviços contratados. Vamos supor que o tutor e o cuidador fecharma por RS: 100. O tutor pagaria 100 e o cuidador receberia 90, por exemplo.

- Plano Tutor: inspirado no club ifood.
	RS 9.99/Mês
	Mais fotos do pet durante a estadia.
	10% de desconto em todos os usos.  Ou seja, o lucro da plataforma seria somente com o plano nesse caso. Embora diminua o lucro imediatamente, aumenta a fidelidde do tutor. 


- Plano cuidador: 
	RS 29.99/mês
	Receberia 100% do valor original por transação
	Selo verificado
	Destaque no catálogo e prioridade de buscas


	Talvez uma assinatura semestral seja util para quem viaja pouco.
![](../attachments/Pasted%20image%2020260509172604.png)


![](../attachments/Pasted%20image%2020260509173229.png)

---

Atue como um UI/UX Designer. Preciso que você crie a interface de um aplicativo mobile focado em tutores de pets (Marketplace de Cuidados Pet).

**Diretrizes Visuais:**
- **Estilo:** Protótipo de baixa fidelidade (Wireframe).
- **Cores:** Utilize exclusivamente paletas acinzentadas (escala de cinza). O foco desta versão é a disposição dos elementos e a usabilidade, sem aplicação de cores finais ou identidade visual complexa.

É UM APLICATIVO MOBILE. USE A PROPORÇÃO 9:16

### Módulo de Autenticação

**Tela de Login:**

- Campo: E-mail
    
- Campo: Senha
    
- Botão: Entrar
    
- Link: Esqueci minha senha
    
- Link: Criar nova conta
    

**Tela de Registro:**

- Campo: Nome completo
    
- Campo: E-mail
    
- Campo: Telefone
    
- Campo: Senha
    
- Campo: Confirmar senha
    
- Botão: Cadastrar
    

### Módulo de Gestão de Pets

**Tela de Lista de Pets:**

- Cards dos pets cadastrados (Foto, Nome, Espécie)
    
- Botão flutuante: Adicionar novo pet
    

**Tela de Cadastro de Pet:**

- Upload: Foto do pet
    
- Campo: Nome
    
- Seleção: Espécie (Cão/Gato)
    
- Campo: Raça
    
- Seleção: Porte (Pequeno, Médio, Grande)
    
- Seleção: Nível de energia (Baixo, Médio, Alto)
    
- Seleção: Sociabilidade
    
- Campo de texto: Restrições alimentares
    
- Campo de texto: Necessidades médicas
    
- Botão: Salvar Pet
    

### Módulo Principal

**Tela Home (Dashboard):**

- Header: Saudação e foto do tutor
    
- Card de Status: Hospedagens ativas ou em andamento
    
- Botão principal 1: Criar Demanda Aberta (Publicar vaga)
    
- Botão principal 2: Explorar Cuidadores (Busca ativa)
    

### Módulo de Demanda Aberta (Opção A)

**Tela de Criação de Demanda:**

- Seleção: Escolher pet cadastrado
    
- Campos de Data/Hora: Check-in (Entrega)
    
- Campos de Data/Hora: Check-out (Retirada)
    
- Campo de texto: Orientações para o período
    
- Campo: Orçamento base sugerido (R$)
    
- Botão: Publicar Demanda
    

**Tela de Gestão de Lances:**

- Lista de propostas recebidas
    
- Dados do Card de Lance: Foto do cuidador, Nome, Nota (Avaliação), Valor cobrado
    
- Ações no Card: Botão "Ver Perfil" e Botão "Aceitar Lance"
    

### Módulo de Busca Ativa (Opção B)

**Tela de Catálogo (Busca):**

- Barra de pesquisa
    
- Filtros: Distância, Nota mínima, Espécie aceita
    
- Lista de cuidadores disponíveis
    
- Dados do Card de Cuidador: Foto, Nome, Nota, Bairro, Preço médio
    
- Ação no Card: Clicar para ver o perfil
    

**Tela de Perfil do Cuidador:**

- Header: Foto, Nome, Selo de Verificado (se assinante)
    
- Métricas: Nota média, Total de serviços concluídos
    
- Galeria: Fotos do ambiente doméstico
    
- Seção: Lista de avaliações em texto de outros tutores
    
- Botão fixo inferior: Enviar Proposta Direta
    

**Tela de Envio de Proposta Direta:**

- Seleção: Escolher pet cadastrado
    
- Campos de Data/Hora: Check-in
    
- Campos de Data/Hora: Check-out
    
- Campo: Valor oferecido (R$)
    
- Botão: Enviar Proposta
    

### Módulo de Acompanhamento (Durante o Serviço)

**Tela de Diário da Estadia (Timeline):**

- Header: Nome do pet, foto miniatura e status da hospedagem (ex: "Em andamento")
    
- Barra de Progresso: Indicador visual do tempo decorrido da estadia (Check-in ao Check-out)
    
- Seção de Conformidade do Cuidador: Checklist visual das janelas de horário (Acordo de Nível de Serviço) para envio de fotos (ex: "Manhã: 08h-10h", "Tarde: 14h-16h", "Noite: 19h-21h")
    
- Linha do Tempo (Timeline): Feed vertical exibindo as fotos enviadas pelo cuidador com o carimbo de data e hora
    
- Indicador de Status: Ícones de "Verificado" (foto enviada no prazo) ou "Pendente/Atrasado" ao lado de cada janela de horário
    
- Ação: Botão flutuante para "Abrir Chat Direto" (com ícone de balão de mensagem)
    

**Tela de Chat Interno:**

- Header: Nome do cuidador e Status da reserva
    
- Área de rolagem: Balões de mensagens
    
- Barra inferior: Campo de digitação
    
- Ação: Botão de anexo (para envio de fotos adicionais ou localização)
    
- Ação: Botão de enviar
    

**Tela de Notificações:**

- Lista de alertas (ex: "Novo lance recebido", "Reserva confirmada", "Lembrete de check-in", "Nova foto recebida no Diário da Estadia")
    

### Módulo Financeiro

**Tela de Checkout (Pagamento):**

- Resumo: Datas, Pet e Cuidador escolhido
    
- Discriminação de valores: Valor do serviço, Taxa da plataforma, Desconto (se assinante), Total a pagar
    
- Seleção: Método de pagamento (Cartão de Crédito, PIX)
    
- Botão: Confirmar Contratação
    

**Tela de Assinatura (Plano Tutor):**

- Lista de Benefícios: "10% de desconto em transações", "SLA mais rígido para envio de fotos"
    
- Card de Opção: Mensal (R$ 15,00)
    
- Card de Opção: Semestral
    
- Botão: Assinar Plano



---

O Sabino pode argumentar: O modelo por demanda e resposta cria um modelo assíncrono, o que quebra a agilidade da contratação e esfria o usuário.

**Justificativas**:
- Um dos maiores causadores de abandono em marketplaces de serviços é a rejeição. Se o tutor precisa enviar 5 propostas e receber 4 respostas negativas (porque o cuidador não aceita cães grandes, ou esqueceu de atualizar a agenda), o fluxo é rápido, mas frustrante. No Mural, cada lance recebido já é um "Match" garantido. O tutor só interage com quem comprovadamente tem vaga, aceita o perfil do animal e concorda com as condições.
- Se o tutor precisa viajar amanhã, o tempo de resposta do Mural será um problema, e por isso ele usará a Busca Ativa. Mas, no contexto de médio prazo, o tutor pode preferir esperar algumas horas para receber várias opções e comparar preços.