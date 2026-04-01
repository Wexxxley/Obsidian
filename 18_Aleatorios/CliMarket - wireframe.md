


---

Wireframe Textual, estruturado formalmente para servir de guia absoluto para o desenvolvimento da interface e do fluxo de dados.

Cores para o wireframe: cinza 1 (escuro), cinza 2(tonalidade média), cinza 3 (claro)

Use icones simples, e somente as caixas (sem curvas) de conteudo com texto generico. 

App mobile. 9:16
## **1. Estrutura de Navegação e Componentes Fixos**

### Top App Bar
- **Ícone de Menu (Esquerda):** Três traços que disparam o Navigation Drawer.
- **Logotipo (Centro):** Espaço para branding da plataforma.
- **Ações (Direita):** Ícone de "Sino" para notificações de novos laudos.
### Breadcrumbs (Trilha de Navegação)
- **Localização:** Barra horizontal fixa logo abaixo da Top App Bar.
- **Componente:** Seta para a esquerda (Voltar) seguida pela trilha de texto (Ex: Início > Clínica X > Agendar).
- **Comportamento:** O texto da tela anterior é clicável para retorno rápido.

### Navigation Drawer 
- **Cabeçalho:** Foto do usuário, Nome Completo e E-mail. 
- **Meus Agendamentos:** Lista de redirecionamentos realizados. 
- **Meus Laudos:** Acesso à central de documentos.
- **Configurações:** Gerenciamento de conta e segurança.
- **Termos de Uso:** Incluindo o consentimento explícito para dados sensíveis.

### Bottom Navigation Bar
- **Início:** Tela de busca de clínicas e serviços.
- **Laudos:** Atalho para visualização de PDFs/Imagens recebidos.
- **Perfil:** Dados cadastrais e histórico de feedbacks.

## 2. Detalhamento das Telas e Componentes (Módulo Paciente)

### A. Tela de Cadastro e Login
- **Campo de Entrada:** Inputs para CPF e Senha.
- **Formulário de Registro:** Nome Completo, CPF, E-mail, Telefone e informaçoes de endereço.
- **Botão de Ação:** "Finalizar Cadastro" que dispara validação de unicidade de dados.
    
- **Modal de Erro (FA01/FA02):**
    - **Título:** "Erro no Cadastro" ou "Acesso Negado".
    - **Conteúdo:** Mensagem indicando CPF já cadastrado/invalido ou senha incorreta.
    - **Botão:** "Tentar Novamente" ou "Recuperar Senha".       

### B. Tela de Busca e Resultados
- **Campo de Pesquisa:** Input superior com lupa para filtrar clínicas e especialidades.
- **LazyRow de Categorias:** Filtros rápidos (Ex: Consultas, Exames, Clínicas Gerais).
- **LazyVerticalGrid (2 Colunas):** Cards de clínicas exibindo imagem, nome, nota e distância.
- **Modal de Localização (FA01):**
    - **Trigger:** GPS desativado.
    - **Conteúdo:** Campo de texto para inserção manual de CEP ou Cidade.
    - **Botão:** "Confirmar Localização".

### C. Tela de Perfil da Clínica
- **Breadcrumbs:** Início > Busca > [Nome da Clínica].
- **Cabeçalho:** Fotos da clínica em carrossel e descrição textual.
- **Aba de Serviços (TabRow):** Lista de consultas e exames com preços.
    
- **Aba de Avaliações:** Lista de feedbacks com notas de 1 a 5 estrelas.
    
- **Modal de Novo Feedback:**
    
    - **Trigger:** Clique em "Avaliar Clínica".
        
    - **Conteúdo:** Seletor de estrelas e campo de texto livre.
        
    - **Validação:** Filtro automático que bloqueia o envio se houver palavras ofensivas.
        

### D. Tela de Agendamento (Redirecionamento)

- **Breadcrumbs:** Início > Clínica > Agendar Serviço.
    
- **Preview da Mensagem:** Texto pré-formatado com os dados do paciente.
    
- **Botão de Confirmação:** "Confirmar e Ir para WhatsApp".
    
- **Modal de Contato Direto (FA01):**
    
    - **Trigger:** Clínica sem link configurado.
        
    - **Conteúdo:** Exibição do número de telefone e botão "Copiar Número".
        

---

## 3. Detalhamento das Telas e Componentes (Módulo Clínica)

### A. Tela de Edição de Perfil

- **Breadcrumbs:** Gestão > Meu Perfil.
    
- **Seção de Dados:** Inputs para horário, localização (mapa) e descrição.
    
- **Gestão de Profissionais:** Lista com botão "+" para novo profissional.
    
- **Gestão de Serviços:** Cadastro de consultas e exames com valores individuais.
    

### B. Tela de Gestão de Laudos

- **Breadcrumbs:** Gestão > Enviar Laudo.
    
- **Busca de Destinatário:** Campo de CPF para localizar o paciente no banco de dados.
    
- **Upload:** Botão para anexar PDF ou Imagem do dispositivo.
    
- **Modal de CPF não Encontrado (FA01):**
    
    - **Conteúdo:** Texto alertando que o paciente não possui cadastro na plataforma.
        
    - **Ação:** Botão "Solicitar que o paciente se cadastre".
        
- **Overlay de Sucesso (MSG01):**
    
    - **Animação:** Check animado verde.
        
    - **Texto:** "Arquivo enviado com sucesso para o paciente".
        
