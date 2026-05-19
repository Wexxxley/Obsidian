

---
### 1. O Problema 
Donos de pets enfrentam barreiras ao precisarem viajar ou se ausentar de suas residências. Em cidades com alto fluxo de estudantes e/ou profissionais que se deslocam entre municípios, como Quixadá, o problema é acentuado.
### 2. A proposta
A proposta consiste em um Marketplace de Cuidado, uma plataforma que conecta tutores a cuidadores locais. A solução utiliza tecnologia para garantir que o ambiente de estadia seja doméstico e adequado ao perfil específico do animal. 

### 3. Fluxo
A ideia é seguir o modelo **Marketplace Orientado à Demanda**.

**A Interface do Tutor** 
Na tela principal do tutor, o sistema deve oferecer três fluxos distintos para a contratação do serviço de hospedagem. 
- **Opção A: Demanda Geral (Mural Aberto)**
    - **Conceito:** O tutor cria um "Card de Demanda" preenchendo um formulário estruturado. Ele informa o período exato (data e hora de entrega/retirada), o perfil detalhado do animal (espécie, porte, nível de energia, sociabilidade) e necessidades específicas (medicação, restrições alimentares). Opcionalmente, pode sugerir um valor base que está disposto a pagar.
    - Este card é publicado em um feed público. Múltiplos cuidadores visualizam a vaga e enviam propostas (lances) com seus respectivos preços. O painel do tutor permite comparar os lances, analisar os perfis dos interessados e aceitar a oferta mais adequada.
        
- **Opção B: Busca Ativa e Proposta Específica**
    - **Conceito:** O tutor acessa um catálogo ou lista de busca para explorar proativamente os perfis dos cuidadores disponíveis na plataforma.
    - **Dinâmica:** O usuário utiliza filtros (como proximidade, tipo de animal aceito ou nota de avaliação) para encontrar um cuidador específico que transmita confiança. Ao acessar o perfil desejado, o tutor clica em enviar uma "Proposta Direta". Ele preenche as datas e necessidades do pet, e esta solicitação é enviada de forma privada e exclusiva para aquele cuidador, que pode aceitar, recusar ou negociar o valor.

**A Interface do Cuidador**
- **Feed de Vagas Públicas:** A interface principal exibe os Cards de Demanda publicados pelos tutores na "Opção A". O cuidador utiliza filtros para visualizar apenas vagas compatíveis com seu perfil (exemplo: "apenas gatos" ou "apenas este fim de semana") e envia suas ofertas de preço para competir pelo serviço.
- **Caixa de Propostas Diretas:** O sistema possui uma área dedicada para solicitações privadas. O cuidador recebe uma notificação isolada, analisa os dados do pet e do período solicitado, e responde.
- **Notificação:** O aplicativo utiliza notificações ativas para manter o cuidador engajado. Se um tutor publica uma demanda geral compatível com as preferências do cuidador, ou se um tutor envia uma proposta direta, o aplicativo emite um alerta.
- **Perfil do Cuidador:** Todo cuidador possui uma página que funciona como seu portfólio. Este perfil exibe sua foto validada, métricas de confiabilidade (nota média e número de serviços concluídos), tipos de animais que aceita hospedar, fotos do ambiente onde o animal ficará e avaliações em texto deixadas por tutores anteriores.

---
### 4. Rentabilidade

- Comissão por Transação (Take Rate): A principal fonte de receita da plataforma é a cobrança de uma comissão sobre os serviços contratados. Vamos supor que o tutor e o cuidador fecharma por RS: 100. O tutor pagaria 100 e o cuidador receberia 90, por exemplo.

- Plano Tutor: inspirado no club ifood.

	RS 15/Mês
	Mais fotos do pet durante a estadia.
	10% de desconto em todos os usos.  Ou seja, o lucro da plataforma seria somente com o plano nesse caso. Embora diminua o lucro imediatamente, aumenta a fidelidde do tutor. 

	Talvez uma assinatura semestral seja util para quem viaja pouco.
![](../attachments/Pasted%20image%2020260509172604.png)

- Plano cuidador: 
	RS 35/mês
	Receberia 100% do valor original por transação
	Selo verificado
	Destaque no catálogo e prioridade de buscas

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

### Módulo de Acompanhamento

**Tela de Notificações:**
- Lista de alertas (ex: "Novo lance recebido", "Reserva confirmada", "Lembrete de check-in")    

**Tela de Chat Interno:**
- Header: Nome do cuidador e Status da reserva
- Área de rolagem: Balões de mensagens
- Barra inferior: Campo de digitação
- Ação: Botão de anexo (para fotos)
- Ação: Botão de enviar
### Módulo Financeiro

**Tela de Assinatura (Plano Tutor):**
- Lista de Benefícios: "10% de desconto em transações", "Mais fotos garantidas"
- Card de Opção: Mensal (R$ 15,00)    
- Card de Opção: Semestral
- Botão: Assinar Plano

**Tela de Checkout (Pagamento):**
- Resumo: Datas, Pet e Cuidador escolhido
- Discriminação de valores: Valor do serviço, Taxa da plataforma, Desconto (se assinante), Total a pagar
- Seleção: Método de pagamento (Cartão de Crédito, PIX)
- Botão: Confirmar Contratação
