

---


Crie um Wireframe para minha aplicação segundo instruções.

Cores para o wireframe: Cinza 1 (Fundo/Textos principais), Cinza 2 (Componentes/Cards), Cinza 3 (Bordas/Inputs).

App mobile. 9:16. 

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
## 2. Detalhamento das Telas e Componentes (visao cliente)

### **A. Tela de Cadastro**
- **Formulário de Registro:** Inputs de texto para Nome Completo, CPF, E-mail, Telefone e campos de endereço (Rua, Número, Bairro, CEP).
- **Botão de Ação:** Botão retangular "Finalizar Cadastro" no rodapé da tela.
- **Modal de Erro (Overlay):**
    - **Título:** "Erro no Cadastro".
    - **Conteúdo:** Mensagem indicando CPF já cadastrado, formato inválido ou dados incompletos.
    - **Botão:** "Tentar Novamente" (fecha o modal para correção dos dados).

### **B. Tela de Login Unificada (Acesso Geral)**

A tela inicial de acesso é dividida por abas para evitar confusão entre o usuário leigo (paciente) e o gestor (clínica).

- **Top App Bar**: Fundo Cinza 1 com o espaço pro logotipo centralizado.
- **Seletor de Perfil (TabRow)**: Duas abas retangulares que ocupam 100% da largura.
    - **Aba 1: "Sou Paciente"**: Selecionada por padrão para o usuário comum.
    - **Aba 2: "Sou Clínica"**: Destinada ao acesso profissional.
#### **1. Aba: Sou Paciente**

- **Campo de Entrada 1**: Input retangular com rótulo "CPF" (Máscara automática: 000.000.000-00).    
- **Campo de Entrada 2**: Input retangular com rótulo "Senha" (Tipo password com ícone de "olho" para mostrar/esconder).
- **Botão de Ação**: Botão retangular em Cinza 1 escrito "Entrar".
- **Link de Navegação**: Texto "Não tem conta? Cadastre-se aqui" que redireciona para a **Tela de Cadastro**.
- **Fluxo de Erro (FA02)**: Caso a senha esteja incorreta, exibe o link "Esqueci minha senha" logo abaixo do campo.
#### **2. Aba: Sou Clínica**

- **Campo de Entrada 1**: Input retangular com rótulo "E-mail Corporativo".
- **Campo de Entrada 2**: Input retangular com rótulo "Senha de Acesso".
- **Botão de Ação**: Botão retangular em Cinza 1 escrito "Acessar Painel Profissional".
- **Aviso de Segurança**: Texto discreto no rodapé: "Acesso restrito a estabelecimentos parceiros. Se sua clínica ainda não está no HealthTech, entre em contato com o suporte: healttack@gmail.com"

- **Modal de Primeiro Acesso (Exclusivo Clínica)**:    
    - **Trigger**: Identificado que a clínica usa a senha gerada por SQL.
    - Texto informado para crar senha segura no primeiro acesso.
    - **Componentes**: Dois campos para "Nova Senha" e "Confirmar Nova Senha".
    - **Regra**: O sistema bloqueia o acesso ao painel até que a senha temporária seja alterada por segurança.


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
    - **Topo**: Foto do perfil da clinica
    - **Centro**: Nome da Clínica em negrito e Nota média (estrelas de 1 a 5).
    - **Base**: Tags retangulares pequenas indicando especialidades principais (Ex: "Cardiologia", "Raio-X").
        
- **Ação de Clique**: Redireciona para o **Perfil Detalhado da Clínica**.
    - **Estado**: Se o usuário acessou esta tela vindo da "Tela de Detalhes da Oferta" (Seção G), o _Breadcrumb_ deve preservar a trilha anterior: `Início > Busca > [Serviço] > Detalhes > [Nome da Clínica]`.

### **I. Tela de Laudos e Resultados**

Espaço restrito para acesso a documentos sensíveis, garantindo a privacidade exigida.

- **Lista de Documentos (LazyColumn)**:
    - **Card de Laudo**:
        - **Lado Esquerdo**: Ícone retangular de "Documento/PDF".
        - **Centro**: Nome do Exame, Data do Upload e Nome da Clínica emissora.
        - **Lado Direito**: Status "Disponível" ou "Novo".
            
- **Ação de Visualização**: Ao clicar, o sistema gera a chave de acesso temporária para o CPF do paciente e abre o visualizador de PDF/Imagem do sistema.

### **J. Tela de Perfil e Configurações**
Área de gestão de dados pessoais e segurança da conta.
- **Seção de Dados Pessoais**: Exibição dos dados cadastrados (Nome, CPF mascarado, E-mail, Telefone, Endereço) com botão "Editar".
- **Gestão de Consentimento**: _Switch_ (chave) para "Autorizo o recebimento de laudos via plataforma", conforme exigência de dados de saúde.
- **Segurança**: Opção para "Alterar Senha" e configuração de Autenticação de Dois Fatores (2FA).
- **Botão de Ação**: Botão retangular Cinza 1 para "Sair da Conta".

---

## 5. Módulo da Clínica: visao paciente
### **K. Perfil Detalhado da Clínica (Visão Paciente)**

Interface completa acessada tanto pela busca de serviços quanto pela aba de Clínicas.

- **Breadcrumbs**: Mantém a trilha de origem (Ex: `Início > Busca > [Serviço] > Detalhes > Clínica` ou `Clínicas > [Nome da Clínica]`).
- **Perfil**: Icone, nome
- Carrossel de fotos retangulares e Descrição textual da infraestrutura.
- **Abas de Conteúdo (TabRow)**:
    - **Aba Informações**: Exibe Localização (mapa simples), Horário de Funcionamento, informaçoes de contato e Corpo Clínico (Lista de nomes e especialidades).
    - **Aba Serviços**: Lista de todas as Consultas e Exames oferecidos com seus respectivos preços.
    - **Aba Avaliações**: Lista de avaliaçoes e botão Avaliar clinica
        
- **Ação de Agendamento**: Botão fixo no rodapé "Agendar via WhatsApp" que carrega a mensagem formatada.

### **M. Fluxo de Avaliação (Feedback do Paciente)**

#### **1. Ponto de Entrada (Trigger)**

- **Localização**: Dentro da aba "Avaliações" do Perfil da Clínica.
- **Componente**: Botão retangular proeminente em **Cinza 1** escrito "Avaliar Clínica".

#### **2. Modal de Avaliação (Overlay)**

Ao clicar no botão, um modal centralizado (sem curvas) sobrepõe a tela atual:
- **Seletor de Nota**: Cinco ícones de estrelas (1 a 5). O paciente clica na estrela correspondente à sua nota; as estrelas selecionadas mudam de **Cinza 3** para **Cinza 1**.
- **Campo de Comentário**: Input de texto multilinha (TextArea) com a etiqueta "Conte-nos sobre sua experiência (opcional)".
- **Botão de Ação**: Botão retangular "Salvar Avaliação".


----

## **6. Visão das clínicas**

### 1. Estrutura de Navegação Fixa

Diferente do paciente, a clínica possui uma navegação focada em gestão operacional.

**Top App Bar**
- **Esquerda**: Nome da Unidade (Ex: "Clínica São José").
- **Centro**: Logo da plataforma
- **Lado Direito**: Etiqueta retangular indicando o Status: "Ativa" ou "Suspensa"

**Bottom  Bar**
- **Painel (Dashboard)**: Ícone de gráfico ou casa, para visão geral.
- **Serviços**: Ícone de lista, para gerenciar o catálogo de preços e profissionais.
- **Laudos**: Ícone de documento, para envios e consulta de histórico (logs).
- **Meu Perfil**: Ícone de engrenagem, para edição de dados institucionais e fotos

### 2. Painel Administrativo da Clínica (Dashboard)

A "Home" do profissional foca em produtividade e alertas rápidos.

- **Cards de Resumo (LazyRow)**:
    - **Serviços Ativos**: Contador total (Ex: "15 Ativos").
    - **Financeiro**: Status de pagamento da mensalidade ("Em dia" ou "Pendente").
    - **Métricas de Busca**: Contador de quantas vezes a clínica apareceu nos resultados dos pacientes.
        
- **Ações Rápidas (Botões Retangulares)**:
    - Botão "Novo Envio de Laudo" (Atalho direto para a tela de upload).
        

### 3. Tela de Gestão de Laudos e Confirmação (Logs)

Esta seção agora inclui o histórico para a clínica ter a prova do cumprimento da obrigação de entrega digital.

#### **A. Tela de Envio de Laudo**
- **Breadcrumbs**: Início > Laudos > Enviar Novo.
- **Componentes do Formulário**:
    - **Campo CPF**: Input retangular com máscara automática (000.**_._**-00).
    - **Validação (FA01)**: Se o CPF não for encontrado, exibe o alerta: "Paciente não cadastrado. O envio só é permitido para usuários da plataforma".
    - **Área de Seleção**: Um retângulo grande para anexar o PDF ou Imagem.
    - **Botão de Ação**: "Confirmar Envio" (Gera a MSG01: "Arquivo enviado com sucesso").

#### **B. Seção de Logs de Envio (Confirmação da Empresa)**

Localizada abaixo do formulário ou em aba separada dentro de "Laudos", permite que a clínica monitore suas atividades passadas.

- **Tabela de Logs (LazyColumn)**:
    - **Data/Hora**: Registro exato do momento do envio.
    - **Destinatário**: Nome do Paciente (Mascarado) e CPF.
    - **Serviço**: Qual exame ou consulta o laudo refere-se.
    
- **Regra de Segurança**: O profissional vê o nome do arquivo enviado e o destinatário, mas o sistema bloqueia a visualização do conteúdo do documento após o envio para proteger a privacidade do paciente.

### 4. Detalhamento da Tela de Edição de Perfil (Visão Clínica)

Esta tela é o espelho administrativo do que o paciente consome. O gestor utiliza esta área para alimentar a "vitrine" da instituição.

#### **A. Identidade Visual e Básica**
- **Foto de Perfil/Logotipo**: Espaço retangular para upload da imagem que aparece nos cards de busca e na grid institucional.
- **Carrossel de Fotos**: Lista horizontal com botão "+" para adicionar fotos da infraestrutura (recepção, salas de exame) que o paciente vê nos "Detalhes da Oferta" e uma botao para excluir do carrosel a imagem.
- **Descrição da Clínica**: Campo de texto multilinha para a biografia e diferenciais da instituição.

#### **B. Localização e Contato**
- **Endereço e Mapa**: Inputs de texto para Ru, Número, Bairro e CEP.
- **Horário de Funcionamento**: Campo de texto para descrição dos turnos (Ex: "Seg a Sex: 08h às 18h").
- **Link de Atendimento**: Campo para inserir o número do WhatsApp ou link do site para o redirecionamento de agendamento.

#### **C. Corpo Clínico (Equipe)**

- **Lista de Profissionais**: Cada item contém dois inputs retangulares: "Nome do Profissional" e "Especialidade".
- **Ação**: Botão "+" em Cinza 2 para adicionar nova linha de profissional e ícone de "Lixeira" para remover.

#### **D. Catálogo de Serviços (Consultas e Exames)**

- **Tabela de Preços**: Estrutura de linhas onde o gestor define o que aparece nos resultados de busca do paciente.
    - **Coluna 1**: Nome do Procedimento (Ex: Hemograma, Consulta Cardiológica).
    - **Coluna 2**: Preço Individual (Input numérico em R$).
        
- **Tags de Especialidade**: Seleção de palavras-chave que aparecerão como "Tags" nos cards da Grid Institucional (Ex: "Raio-X", "Pediatria").

### **Botão de Ação e Persistência**

- **Botão**: "Salvar Alterações"  fixo.
    
- **Mensagem (MSG01)**: Overlay centralizado com o texto "Perfil atualizado com sucesso" após a validação dos dados.
