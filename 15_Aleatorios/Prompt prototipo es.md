

---
### **Visão Geral e Estilo de Design (Design System)**

- Projeto: "Acervo Mestre" - Um repositório centralizado de conteúdo pedagógico.
- Logo (Obrigatório): O design DEVE usar o logo "Acervo Mestre" fornecido.
- Estilo Visual (Crítico): O design deve ser profissional, limpo, minimalista e acadêmico, seguindo o layout do wireframe fornecido (painel lateral esquerdo estático, conteúdo rolável à direita).

---
### **Paleta de Cores (Crítico: Paleta Neutra - Light Mode)**

- **Fundos (Branco/Neutro):**
    - Fundo da Página (Base): Um cinza muito claro ou branco (ex: `#F8F9FA`).
    - Fundo de Superfícies (Painel Lateral, Cards, Modais): Branco puro (ex: `#FFFFFF`).
        
- **Textos (Preto/Neutro):**
    - Títulos / Texto Principal: Um cinza muito escuro, quase preto (ex: `#212529`).
    - Texto Secundário / Descrições / placeholders: Cinza médio (ex: `#6C757D`).
        
- **Bordas/Divisores:** Cinza claro (ex: `#DEE2E6` ou `#E0E0E0`).
    
- **Cor de Acento (Apenas para Detalhes):**
    - Usar o **azul-escuro/teal do logo**. APENAS para elementos interativos principais: botões primários ("Entrar", "Salvar"), links, ícones de navegação ativos, e foco de formulário (focus-ring).
        
- **Cores Semânticas:**
    - Destaque (Estrela): Amarelo/Dourado (ex: `#FFD700`).
    - Curtir (Coração): Vermelho claro (ex: `#E53935`).

---
### **Tipografia**
- Fonte: Usar uma fonte Sans-serif clara, moderna e legível (ex: Inter, Roboto, ou Lato).
- Hierarquia: Usar pesos de fonte distintos para títulos (Bold), subtítulos (Semibold) e texto corrido (Regular).

---
### **Perfis de Usuário (Define a Visibilidade dos Controles)**

O design deve refletir 4 modos de visualização baseados no perfil:

- Gestor (Admin): Vê tudo. Tem acesso ao "Painel de Administração" no menu lateral.
- Coordenador (Moderador): Vê tudo (Público/Privado). Vê botões "Adicionar Recurso", "Criar Playlist". Pode "Editar", "Excluir" e "Marcar como Destaque" qualquer recurso.
- Professor (Criador): Vê tudo (Público/Privado). Vê botões "Adicionar Recurso", "Criar Playlist". Só pode "Editar" e "Excluir" os seus próprios recursos.
- Aluno (Consumidor): Visão mais simples. Vê apenas recursos "Públicos". Não vê botões de admin, edição ou criação. Pode "Curtir" e "Baixar".

---
### **Componente Principal (Resource Card)**

Criar um componente "Card de Recurso" padronizado bordas arredondadas).

**Conteúdo do Card:**
- Título (em branco, fonte bold).
- Nome do Autor (em cinza claro, fonte menor).
- Ícone indicando o tipo (PDF, URL, Nota Simples).
- Tags (em formato de "pills" ou emblemas
- Métricas (Ícone de olho para visualizações, ícone de download, ícone de coração para curtidas).
- Controles no Card (Visíveis no Hover, baseados no perfil):
	- Coordenador: Ícone de Estrela (Destaque), Editar, Excluir.
	- Professor (se for autor): Editar, Excluir.
- Todos: Ícone de "Adicionar à Playlist".

---
### **Telas Principais (Wireframes de Alta Fidelidade)**

**A. Tela de Login (RF01)**
Conteúdo: Logo "Acervo Mestre" centralizado no topo. Formulário centralizado com campos "E-mail Institucional" e "Senha". Link "Esqueci minha senha".

(Nota: O cadastro é feito pelo Gestor, então não há link de "Cadastre-se").

**B. Tela Inicial / Dashboard (Layout do Wireframe - Crítico)**
Layout Geral: Um Painel de Navegação Estático à esquerda e uma área de conteúdo principal à direita. As seções de conteúdo terão rolagem horizontal.

**Painel Estático (Esquerda):**
- Logo "Acervo Mestre" no topo.
- Links de navegação com ícones (ex: Início, Minhas Playlists, Meu Perfil, Painel de Administração). O ícone ativo deve usar a cor de acento azul.

- "Painel de Administração" (visível apenas para Gestor).
- Link "Sair" na parte inferior.

**Área de Conteúdo (Direita):**

- Header da Área: Contém a Barra de Busca. Placeholder: "Procurar por conteudo".
- Tags: Abaixo da barra de busca, exibir as opções de tag ("Matéria", "Formato", "tags") (tags fixas gerenciadas pelo Gestor) em formato de pilula.

**Seções de Conteúdo (Carrosséis):**

DESTAQUE: Título da seção. Abaixo, um carrossel de "Cards de Recurso" com scroll horizontal (overflow-x: auto).

MAIS CURTIDOS: Título da seção. Abaixo, um carrossel de "Cards de Recurso" com scroll horizontal.

RECENTES: Título da seção. Abaixo, um carrossel de "Cards de Recurso" com scroll horizontal.

Botão de Ação (FAB): (Visível apenas para Professor/Coordenador) Um botão flutuante no canto inferior direito com um ícone de "+" para "Adicionar Recurso" (usar cor de acento azul).

Todo esse conteudo deve ser mostrado na tela sem precisar de rolagem vertical (não é para ter rolagem vetical na tela inicial)

**C. Página de Detalhes do Recurso (RF17, RF19, RF20)**

Layout: Ao clicar em um card, mostrar esta tela.

Conteúdo:

Título grande.

Nome do Autor (clicável para "Página do Autor").

Visualizador (Decisão de Requisito):

Se for "Nota Simples" (RF06) ou "PDF": Exibe o conteúdo renderizado (Markdown) ou um visualizador de PDF embutido.

Se for "Upload" (DOCX, PPTX) ou "URL" (RF05): Mostra um ícone grande, a descrição e o botão "Baixar Recurso" ou "Acessar Link" (pois a visualização nativa não é suportada, exceto PDF/Nota).

Metadados: Botões "Curtir" (Coração), "Adicionar à Playlist". Métricas (Visualizações, Downloads, Curtidas). Seção de Tags. Descrição completa.

**D. Formulário de Adicionar/Editar Recurso (RF04, RF05, RF06, RF07, RF11)**

Layout: Um modal

Seleção de Tipo (Tabs): "Upload de Arquivo", "Link Externo", "Nota Simples".

Campos Comuns: "Título", "Descrição", "Tags" (campo de seleção/autocomplete com as tags fixas), "Privacidade" (RF07 - Toggle ou Botões de rádio: "Público - Visível para Alunos", "Privado - Apenas Professores/Coord.").

Campos Específicos:

Tab "Upload": Área de "arrastar e soltar" (dropzone).

Tab "Link Externo": Campo para a "URL".

Tab "Nota Simples": Editor de texto Markdown (react-markdown).

Botões: "Salvar Recurso" (com acento azul).

**E. Página do Autor (RF19)**

Layout: Uma página de perfil.

Header: Avatar, Nome Completo, E-mail Institucional, perfil(aluno, gestor, etc).

Tabs: "Recursos" e "Playlists" (mostrando apenas os itens criados por esse autor).

Conteúdo: Um grid padrão de "Cards de Recurso" ou "Cards de Playlist".

**F. Painel de Administração (Apenas Gestor - RF02, RF03, RF22)**

Layout: Funcional, baseado em tabelas **(seguindo a paleta Light Mode definida)**.

Navegação (Tabs): "Gestão de Usuários", "Gestão de Metadados".

Tab "Gestão de Usuários": Botão "Cadastrar Novo Usuário" (RF02). Tabela de usuários com ações de "Desativar/Ativar" (RF03) e "Editar Perfil".

Tab "Gestão de Metadados" (RF22): Seções para gerenciar as tags fixas (ex: "Matérias", "Séries", "Formatos"). Cada seção deve ter um campo "Adicionar novo..." e uma lista dos itens existentes com botões de "Editar" e "Excluir".

