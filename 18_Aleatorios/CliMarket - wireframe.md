

---


Crie um Wireframe para minha aplicação segundo instruções.

Cores para o wireframe: cinza 1 (escuro), cinza 2(tonalidade média), cinza 3 (claro)

Use icones simples, e somente as caixas (sem curvas).

App mobile. 9:16. 360*640

## **1. Estrutura de Navegação e Componentes Fixos**

### Top App Bar
- **Ícone de Menu (Esquerda):** Três traços que disparam o Navigation Drawer.
- **Logotipo (Centro):** Espaço para branding da plataforma.
- **Direita:** Ícone de "Sino" para notificações de novos laudos.
### Breadcrumbs (Trilha de Navegação)
- **Localização:** Barra horizontal fixa logo abaixo da Top App Bar. Tome cuidado para não ficar grande, quero algo pequeno.
- **Componente:** Seta para a esquerda (Voltar) seguida pela trilha de texto (Ex: Início > Clínica X > Agendar). As telas iniciais (busca, laudo, perfil), não possui nada, afinal, ela são as iniciais
- **Comportamento:** O texto da tela anterior é clicável para retorno rápido.
### Navigation Drawer 
- Ocupado 50% da parte horizontal da tela.
- **Cabeçalho:** Foto do usuário, Nome Completo e E-mail. 
- **Meus Agendamentos:** Lista de redirecionamentos realizados. 
- **Configurações:** Gerenciamento de conta e segurança.
- **Termos de Uso:** Incluindo o consentimento explícito para dados sensíveis.
### Bottom Navigation Bar
- **Início:** Tela de busca de clínicas e serviços.
- **Laudos:** Atalho para visualização de PDFs/Imagens recebidos.
- **Perfil:** Dados cadastrais e histórico de feedbacks.

## 2. Detalhamento das Telas e Componentes

### A. Tela de Cadastro

- **Formulário de Registro:** Nome Completo, CPF, E-mail, Telefone e informaçoes de endereço.
- **Botão de Ação:** "Finalizar Cadastro"
    
- **Modal de Erro:**
    - **Título:** "Erro no Cadastro"
    - **Conteúdo:** Mensagem indicando CPF já cadastrado/invalido ou senha incorreta.
    - **Botão:** "Tentar Novamente".       

### B. Tela de Login
- **Campo de Entrada:** Inputs para CPF e Senha.

### C. Detalhamento da Tela Inicial (Funil de Intenção)
#### **A. Estrutura de Navegação Superior** 
- **Top App Bar:** Ícone de menu (esquerda), Identidade Visual (centro) e Foto de Perfil (direita).
    
- **Saudação Personalizada:** Texto em destaque: "Olá, [Nome], o que você busca hoje?".
    

### B. Seção de Seleção Primária (Cards de Grande Formato)

Em vez de uma lista genérica, o usuário escolhe o "Caminho" logo no topo da tela:

- **Card "Preciso de Consulta":** Card com ícone de estetoscópio. Ao clicar, abre o **Modal de Especialidades**.
    
- **Card "Preciso de Exame":** Card com ícone de frasco de ensaio/raio-x. Ao clicar, abre o **Modal de Tipo de Exame**.
    

### C. Modais de Fluxo Sequencial (O "Cérebro" da Tela)

#### 1. Modal de Especialidades (Caminho: Consulta)

- **Trigger:** Clique no Card "Consulta".
    
- **Conteúdo:** * Barra de busca interna: "Qual especialidade?" (ex: Cardiologia).
    
    - **LazyVerticalGrid (3 colunas):** Ícones circulares com texto abaixo para as especialidades mais comuns (Pediatria, Clínica Geral, etc).
        
    - **Ação:** Ao selecionar, o modal fecha e a tela de resultados carrega as clínicas que atendem essa especialidade.
        

#### 2. Modal de Tipo de Exame (Caminho: Exame)

- **Trigger:** Clique no Card "Exame".
    
- **Passo 1 (Subtipo):** Dois botões grandes: "Laboratorial" (sangue, urina) ou "Imagem" (Raio-X, Ultrassom).
    
- **Passo 2 (Especificação):** Após escolher o subtipo, abre-se uma lista/busca para o exame específico (ex: "Hemograma" ou "Ressonância").
    
- **Ação:** Ao selecionar o exame específico, a tela de resultados carrega as clínicas/laboratórios que realizam o procedimento.
    

### D. Seção de Localização Automática (Barra de Contexto)

- **Componente:** Uma barra fina logo abaixo dos Cards Primários indicando: "Mostrando resultados para: **[Nome da Rua/Bairro ou Cidade]**".
    
- **Ícone de Lápis:** Permite alterar o local manualmente caso o GPS falhe (FA01).
    

---

## 4. Detalhamento da Tela de Resultados (Pós-Seleção)

Após o usuário completar o fluxo sequencial acima, os resultados aparecem seguindo esta ordem:

### A. Cabeçalho de Filtro Ativo

- **Breadcrumbs:** Início > Busca > [Especialidade ou Exame Selecionado].
    
- **Tag de Filtro:** Um "chip" destacado no topo indicando o que foi filtrado (ex: "Exame: Laboratorial - Hemograma"). Um ícone de "X" no chip permite voltar ao início.
    

### B. Listagem de Clínicas (LazyColumn)

Para leigos, cards de largura total são melhores para leitura do que grades de 2 colunas:

- **Card de Clínica/Laboratório:**
    
    - **Lado Esquerdo:** Foto da fachada ou logotipo.
        
    - **Centro:** Nome da Clínica, nota em estrelas e distância.
        
    - **Lado Direito (Destaque):** Preço do serviço específico selecionado (ex: "R$ 45,00").
        
    - **Rodapé do Card:** Botão "Ver Detalhes".
        

---

## 5. Componentes de Erro e Suporte na Tela Inicial

### Modal de Localização Obrigatória (FA01)

- **Trigger:** Usuário tenta selecionar uma categoria sem o GPS estar ativo e sem local definido.
    
- **Conteúdo:** Texto "Precisamos saber onde você está para encontrar as clínicas mais próximas".
    
- **Input:** Campo para digitar o CEP.
    

### Modal de "Clínica não encontrada" (MSG01)

- **Trigger:** Nenhuma clínica na região oferece a especialidade ou exame selecionado.
    
- **Conteúdo:** "Não encontramos clínicas para [Serviço] em [Localidade]".
    
- **Ação:** Botão "Tentar outra localização" ou "Falar com suporte".
    



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
        
