

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
- **Ações:** Botão "Entrar" e link "Criar conta" (direciona para a Tela de Cadastro).

### C. Detalhamento da Tela Inicial (Funil de Intenção)

- **Saudação Personalizada:** Texto em destaque: "Olá, [Nome], o que você busca hoje?".  
#### 1. Seção de Seleção Primária (Cards de Grande Formato)
- **Card "Preciso de Consulta":** Card com ícone de estetoscópio. Ao clicar, abre a tela de Especialidades.
- **Card "Preciso de Exame":** Card com ícone de frasco de ensaio. Ao clicar, abre a tela de Tipo de Exame.

#### 2. tela de Especialidades (Caminho: Consulta)
- Breadcrumbs
- **Conteúdo:**  Barra de busca interna: "Qual especialidade?" (ex: Cardiologia).
- **LazyVerticalGrid (2 colunas):** Ícones circulares com texto ao lado para as especialidades comuns (Pediatria, Clínica Geral, cardilogia, ginecologia, etc).  
- Ao selecionar, o modal fecha e a tela de resultados carrega os componentes de  consutas.
#### 3. tela de Tipo de Exame (Caminho: Exame)
- Breadcrumbs
- **Subtipo:** Dois botões grandes: "Laboratorial" (sangue, urina) ou "Imagem" (Raio-X, Ultrassom).
- Após escolher o subtipo
	- Barra de busca interna: "Qual exame?"
	- **LazyVerticalGrid (3 colunas):** Ícones circulares com texto abaixo para os exames. Hemograma, Ressonância e etc...
- Ao selecionar, o modal fecha e a tela de resultados carrega os componentes de exames.

---

## 4. Tela de Resultados (Pós-Seleção)

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
        
