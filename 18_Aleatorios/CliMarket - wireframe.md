

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
- **Interatividade de Clínica:** Link "Ver Perfil desta Clínica" para acessar o catálogo completo institucional sem perder o filtro de busca atual.
    
- **Botão de Ação:** "Agendar via WhatsApp".
    
- **Modal de Redirecionamento:** Exibe a mensagem pré-definida com dados do paciente e o serviço desejado antes de abrir o aplicativo externo.
    

---

## 4. Seções Adicionais e Gestão

### **H. Tela de Clínicas (Busca Institucional)**

- **Breadcrumbs:** Clínicas.
    
- **Barra de Busca:** Input "Pesquisar clínica pelo nome".
    
- **Grid (2 colunas):** Cards institucionais com foto da fachada, nome da clínica, tags de especialidades e nota média.
    
- **Ação:** Abre o Perfil da Clínica, listando todos os serviços e corpo clínico.
    

### **I. Gestão de Laudos (Módulo Clínica)**

- **Breadcrumbs:** Gestão > Enviar Laudo.
    
- **Busca de Destinatário:** Input para inserir o CPF do paciente.
    
- **Upload:** Botão "Anexar PDF/Imagem".
    
- **Modal de Erro (FA01):** "CPF não encontrado na base de dados".
    
- **Overlay de Sucesso (MSG01):** Check animado com texto "Arquivo enviado com sucesso".
    

### **J. Modal de Localização Obrigatória (FA01)**

- **Trigger:** Disparado se o usuário tentar buscar serviços com o GPS desativado.
    
- **Conteúdo:** "Precisamos saber onde você está para encontrar as clínicas mais próximas".
    
- **Input:** Campo para inserção manual do CEP.




----







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
- **Início:** Funil de intenção (Consultas/Exames).
- **Clínicas:** Seção para busca e listagem direta de estabelecimentos.
- **Laudos:** Acesso aos resultados digitalizados.
- **Perfil:** Dados do paciente e configurações.

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

#### 1. Seção de Seleção Primária (Cards de Grande Formato)
- **Saudação Personalizada:** Texto em destaque: "Olá, [Nome], o que você busca hoje?".  
- **Card "Preciso de Consulta":** Card com ícone de estetoscópio. Ao clicar, abre a tela de Especialidades.
- **Card "Preciso de Exame":** Card com ícone de frasco de ensaio. Ao clicar, abre a tela de Tipo de Exame.

#### 2. tela de Especialidades (Caminho: Consulta)
- **Conteúdo:**  Barra de busca interna: "Qual especialidade?" (ex: Cardiologia).
- Breadcrumbs: Início > Especialidades.
- grid (2 colunas): Ícones circulares com texto ao lado para as especialidades (Pediatria, Clínica Geral, cardilogia, ginecologia, etc).  
- Ao clicar, abre a Tela de Resultados de Consultas para aquela especialidade.
#### 3. tela de Tipo de Exame (Caminho: Exame)
- **Breadcrumbs:** Início > Exames.
- **Barra de Busca Superior:** Input de texto com a etiqueta "Qual exame você procura?" (Ex: Hemograma, Ressonância).
- **Seleção de Subtipo (Filtros Alternados):** Dois botões de destaque (Chips) posicionados logo abaixo da busca:
    - **Botão "Laboratorial":** Ao ser ativado, filtra a grade apenas para exames de análise clínica (sangue, urina, etc.) e desativa automaticamente o filtro "Imagem".
    - **Botão "Imagem":** Ao ser ativado, filtra a grade para procedimentos radiológicos (Raio-X, Ultrassom, etc.) e desativa automaticamente o filtro "Laboratorial".
    - **Estado Neutro:** Se o usuário clicar no filtro ativo para desativá-lo, a grade volta a exibir todos os tipos de exames disponíveis.
        
- grid (2 colunas): Ícones circulares com texto ao lado para os exames.
- Ao clicar, abre a Tela de Resultados de Exames para aquela especialidade.

### 4. Tela de Resultados (Pós-Seleção)

Nesta tela, o foco não é a clínica, mas sim as ofertas do serviço selecionado em diferentes locais para comparação.

#### A. Listagem de Ofertas (LazyColumn)

- **Breadcrumbs:** Início > Busca > [Nome do Exame ou Especialidade].
- **Card de Oferta de Serviço:**
    - **Topo:** Nome do Serviço em destaque (Ex: "Hemograma Completo").
    - **Corpo (Lado Esquerdo):** Logo da Clínica que oferece o serviço.
    - **Corpo (Centro):** Nome da Clínica, nota de avaliação e distância.
    - **Corpo (Lado Direito):** Preço do serviço naquela clínica específica (Ex: "R$ 45,00").
    - **Botão de Ação:** "Ver Detalhes".

#### E. Tela de Detalhes da Oferta (Ao clicar no Card)
- **Breadcrumbs:** Início > Busca > [Nome do Exame ou Especialidade] > Detalhes 
- **Informações do Serviço:** Descrição do que está incluso no exame ou consulta.
- **Informações da Clínica:** Endereço, horário e fotos do local.
- **Botão:** "Agendar via WhatsApp".

### 4. Tela de Clínicas (Bottom Bar)

F. Busca Institucional
- **Breadcrumbs:** Clínicas.
- **Barra de Busca:** "Pesquisar clínica pelo nome".
- **LazyVerticalGrid (2 colunas):** Cards focados na instituição:
    - Foto da fachada.

    - Nome da Clínica.
        
    - Especialidades atendidas (Tags).
        
    - Nota média de avaliação.
        
- **Ação:** Ao clicar, abre o **Perfil da Clínica**, que lista todos os serviços disponíveis e corpo clínico.
## 5. Componentes de Erro e Suporte na Tela Inicial

### Modal de Localização Obrigatória (FA01)

- **Trigger:** Usuário tenta selecionar uma categoria sem o GPS estar ativo e sem local definido.
    
- **Conteúdo:** Texto "Precisamos saber onde você está para encontrar as clínicas mais próximas".
    
- **Input:** Campo para digitar o CEP.



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
        
