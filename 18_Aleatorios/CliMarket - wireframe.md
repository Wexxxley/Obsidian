

---


Crie um Wireframe para minha aplicação segundo instruções.

Cores para o wireframe: Cinza 1 (Fundo/Textos principais), Cinza 2 (Componentes/Cards), Cinza 3 (Bordas/Inputs).

Use icones simples, e somente as caixas (sem curvas).

App mobile. 9:16. 360 * 640px

## 1. Estrutura de Navegação e Componentes Fixos

### **Top App Bar**    
- **Ícone de Menu (Lado Esquerdo):** Quadrado com três traços horizontais simples que dispara o _Navigation Drawer_.
- **Logotipo (Centro):** Espaço retangular para branding da plataforma.
- **Notificações (Lado Direito):** Ícone de "Sino" para sinalizar novos laudos disponíveis.

### **Breadcrumbs (Trilha de Navegação)**
- **Localização:** Barra horizontal fina fixada logo abaixo da _Top App Bar_.    
- **Componente:** Seta para a esquerda (Botão Voltar) seguida pela trilha de texto (Ex: Início > Clínica X > Agendar). Tome cuidado como tamanho, deixe pequeno essa barra.
- **Regra de Exibição:** Oculta nas telas iniciais (Busca, Clínicas, Laudos, Perfil). Torna-se visível apenas ao aprofundar a navegação.
- **Interatividade:** O texto da tela anterior na trilha é clicável para retorno rápido. 

### **Navigation Drawer (Menu Lateral)**
- **Dimensão:** Ocupa 50% da largura horizontal da tela.
- **Cabeçalho:** Foto do usuário (quadrada), Nome Completo e E-mail.
- **Itens de Menu:**
    - **Meus Agendamentos:** Lista cronológica de redirecionamentos realizados para clínicas.
    - **Configurações:** Gerenciamento de conta, senha e dados de perfil.
    - **Termos de Uso:** Texto jurídico incluindo o consentimento explícito para tratamento de dados sensíveis e laudos.

### **Bottom Navigation Bar**
- **Início:** Funil de intenção (Consultas e Exames).
- **Clínicas:** Seção dedicada à busca e listagem direta de estabelecimentos.
- **Laudos:** Acesso centralizado aos resultados de exames digitalizados e enviados pelas clínicas.
- **Perfil:** Gestão de dados pessoais do paciente e configurações de privacidade.

---
## 2. Detalhamento das Telas e Componentes

### **A. Tela de Cadastro**
- **Formulário de Registro:** Inputs de texto para Nome Completo, CPF, E-mail, Telefone e campos de endereço (Rua, Número, Bairro, CEP).
- **Botão de Ação:** Botão retangular "Finalizar Cadastro" no rodapé da tela.
- **Modal de Erro (Overlay):**
    - **Título:** "Erro no Cadastro".
    - **Conteúdo:** Mensagem indicando CPF já cadastrado, formato inválido ou dados incompletos.
    - **Botão:** "Tentar Novamente" (fecha o modal para correção dos dados).

### **B. Tela de Login**
- **Campos de Entrada:** Inputs para CPF e Senha.
- **Ações:** Botão "Entrar" em Cinza 1 e link de texto "Criar conta" que redireciona para a Tela de Cadastro.

### **C. Tela Inicial (Funil de Intenção)**
- **Saudação Personalizada:** Texto em destaque no topo: "Olá, [Nome], o que você busca hoje?".
    
- **Seção de Seleção Primária (Cards de Grande Formato):**
    - **Card "Preciso de Consulta":** Card retangular Cinza 2 com ícone de estetoscópio. Ao clicar, abre a tela de Especialidades.
    - **Card "Preciso de Exame":** Card retangular Cinza 2 com ícone de frasco de ensaio. Ao clicar, abre a tela de Tipo de Exame.

### **D. Tela de Especialidades (Caminho: Consulta)**
- **Breadcrumbs:** Início > Especialidades.
- **Barra de Busca Interna:** Input "Qual especialidade?" (Ex: Cardiologia).
- **Grid (2 colunas):** Cards com ícone circular e texto lateral indicando a especialidade (Pediatria, Clínica Geral, Cardiologia, Ginecologia, etc).
- **Ação:** Ao clicar, abre a Tela de Resultados de Consultas filtrada pelo serviço escolhido.

### **E. Tela de Tipo de Exame (Caminho: Exame)**
- **Breadcrumbs:** Início > Exames.
- **Barra de Busca Superior:** Input "Qual exame você procura?" (Ex: Hemograma, Ressonância).
- **Seleção de Subtipo (Chips de Filtro):**
    - **Botão "Laboratorial":** Ao ativar, filtra exames de análise clínica e desativa o filtro "Imagem".
    - **Botão "Imagem":** Ao ativar, filtra exames radiológicos e desativa o filtro "Laboratorial".
    - **Estado Neutro:** Sem filtros ativos, exibe todos os exames na grade.
    
- **Grid (2 colunas):** Ícones circulares com texto lateral para os exames específicos.

---

## 3. Resultados e Detalhamento de Ofertas

### **F. Tela de Resultados (Listagem de Ofertas)**
- **Foco:** Comparação de preços e locais para o serviço selecionado.
- **Breadcrumbs:** Início > Busca > [Nome do Exame ou Especialidade].
- **Card de Oferta (LazyColumn):**
    - **Topo:** Nome do Serviço em destaque.
    - **Lado Esquerdo:**  Preço do serviço em Cinza 1 (Ex: "R$ 45,00").
    - **Centro:** Nome da Clínica, nota de avaliação (estrelas) e distância.
    - **Lado Direito:**  Logo da Clínica que oferece o serviço.
    - **Botão de Ação:** "Ver Detalhes".

### **G. Tela de Detalhes da Oferta**
- **Breadcrumbs:** Início > Busca > [Serviço] > Detalhes.
- **Informações do Serviço:** Bloco de texto detalhando o que está incluso e orientações de preparo.
- **Informações da Clínica:** Endereço, horário de funcionamento e logo da clinica.
- **Interatividade de Clínica:**  Ao clicar no componente da clinica é redirecionado para o perfil da clinica mas sem perder o estado do breadcrumbs
- **Botão de Ação:** "Agendar via WhatsApp".


## 4. Detalhamento das Telas: Clínicas, Laudos e Perfil

### **H. Tela de Clínicas (Busca Institucional - Aba Bottom Bar)**

Esta tela é o ponto de entrada para quem busca uma instituição específica, independentemente de um exame já selecionado.

- **Breadcrumbs**: Oculto na tela inicial da aba. Torna-se `Clínicas > [Nome da Clínica]` ao acessar o perfil.
    
- **Barra de Busca**: Input retangular "Pesquisar clínica pelo nome".
    
- **Grid (2 colunas)**: Cards focados na identidade da clínica:
    
    - **Topo**: Foto da fachada ou recepção em tons de Cinza 2.
        
    - **Centro**: Nome da Clínica em negrito e Nota média (estrelas de 1 a 5).
        
    - **Base**: Tags retangulares pequenas indicando especialidades principais (Ex: "Cardiologia", "Raio-X").
        
- **Ação de Clique**: Redireciona para o **Perfil Detalhado da Clínica**.
    
    - **Estado**: Se o usuário acessou esta tela vindo da "Tela de Detalhes da Oferta" (Seção G), o _Breadcrumb_ deve preservar a trilha anterior: `Início > Busca > [Serviço] > Detalhes > [Nome da Clínica]`.
        

### **I. Tela de Laudos e Resultados (Aba Bottom Bar)**

Espaço restrito para acesso a documentos sensíveis, garantindo a privacidade exigida.

- **Breadcrumbs**: Início > Laudos.
    
- **Lista de Documentos (LazyColumn)**:
    
    - **Card de Laudo**:
        
        - **Lado Esquerdo**: Ícone retangular de "Documento/PDF".
            
        - **Centro**: Nome do Exame, Data do Upload e Nome da Clínica emissora.
            
        - **Lado Direito**: Status "Disponível" ou "Novo".
            
- **Ação de Visualização**: Ao clicar, o sistema gera a chave de acesso temporária para o CPF do paciente e abre o visualizador de PDF/Imagem do sistema.
    
- **Segurança**: O Administrador do sistema não possui acesso a esta visualização.
    

### **J. Tela de Perfil e Configurações (Aba Bottom Bar)**

Área de gestão de dados pessoais e segurança da conta.

- **Breadcrumbs**: Início > Perfil.
    
- **Seção de Dados Pessoais**: Exibição dos dados cadastrados (Nome, CPF mascarado, E-mail, Telefone, Endereço) com botão "Editar".
    
- **Gestão de Consentimento**: _Switch_ (chave) para "Autorizo o recebimento de laudos via plataforma", conforme exigência de dados de saúde.
    
- **Segurança**: Opção para "Alterar Senha" e configuração de Autenticação de Dois Fatores (2FA).
    
- **Botão de Ação**: Botão retangular Cinza 1 para "Sair da Conta".
    

---

## 5. Módulo da Clínica: Gestão de Informações e Documentos

### **K. Perfil Detalhado da Clínica (Visão Paciente)**

Interface completa acessada tanto pela busca de serviços quanto pela aba de Clínicas.

- **Breadcrumbs**: Mantém a trilha de origem (Ex: `Início > Busca > [Serviço] > Detalhes > Clínica` ou `Clínicas > [Nome da Clínica]`).
    
- **Cabeçalho**: Carrossel de fotos retangulares e Descrição textual da infraestrutura.
    
- **Abas de Conteúdo (TabRow)**:
    
    - **Aba Informações**: Exibe Localização (mapa simples), Horário de Funcionamento e Corpo Clínico (Lista de nomes e especialidades).
        
    - **Aba Serviços**: Lista de todas as Consultas e Exames oferecidos com seus respectivos preços.
        
    - **Aba Avaliações**: Lista de comentários e notas deixadas por outros pacientes.
        
- **Ação de Agendamento**: Botão fixo no rodapé "Agendar via WhatsApp" que carrega a mensagem formatada.
    

### **L. Painel da Clínica (Gestão de Laudos - Visão Profissional)**

Interface exclusiva para funcionários da clínica realizarem a entrega digital.

- **Breadcrumbs**: Painel Clínica > Documentos > Enviar Laudo.
    
- **Área de Seleção**:
    
    1. **Campo CPF**: Input para digitar o CPF do paciente destinatário.
        
    2. **Upload**: Botão "Selecionar Arquivo" (PDF/Imagem).
        
- **Validação (FA01)**: Se o CPF não estiver cadastrado, exibe Overlay: "Paciente não encontrado. Solicite o cadastro antes de enviar".
    
- **Confirmação**: Botão "Confirmar Envio" que dispara a MSG01: "Arquivo enviado com sucesso para o paciente".
    

---