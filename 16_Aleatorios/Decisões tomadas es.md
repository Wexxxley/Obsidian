
---

- O gestor vai realizar o cadastro do usuario e ele vai receber um recebe um email para definir sua senha.

- Para os arquivos de upload(PDF, SLIDES, etc) teremos uma tabela com metadados dos arquivos. E o armazenamento real ficaria por conta do **MinIO**. O MinIO é um **serviço de armazenamento de objetos auto-hospedado (self-hosted)**. Pense nele como se você pudesse rodar a sua própria "Amazon S3" no seu próprio servidor.

- Para o markdown no front podemos usar a biblioteaca **react-markdown.**  O ecossistema de plugins do react-markdown facilitará muito a renderização desses elementos de forma bonita e funcional.

- Tags serão fixas e _padronizados_ pelo gestor ("Matéria",  "Formato"). 

- O gestor/coordenadoor tem que ter a possibilidade de marcar e desmarcar como destaque um recurso.

- Buscar Recursos por Palavra-Chave (TAG, TITULO OU DESCRICAO, nome do autor)

- So é possivel visualizar nativamente na plataforma PDF E NOTAS SIMPLES, o resto é somente download

- Ao clicar no nome do autor de um recurso, sera aberto uma tela, a tela do autor.

- **Padrao de Arquitetura MVC (Model-View-Controller):** É um padrão de arquitetura que separa a aplicação em três componentes principais: Modelo (dados e lógica de negócio), Visão (interface do usuário/Frontend) e Controlador (recebe requisições e coordena Modelo e Visão)."
- model/ controller/ routes/ server.js app.js
- **DTO** (Data Transfer Object),"É um padrão de design (ou objeto) usado para transferir dados entre as camadas da aplicação. 

---
### **TELA INICIAL**
![](../attachments/Pasted%20image%2020251022165352.png)

---
### SQL
```sql

CREATE TABLE "User" (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    senha_hash VARCHAR(255) NOT NULL,
    
    perfil VARCHAR(50) NOT NULL CHECK (perfil IN ('Gestor', 'Coordenador', 'Professor', 'Aluno')),
    status VARCHAR(50) NOT NULL CHECK (status IN ('Ativo', 'Inativo')) DEFAULT 'Ativo',
    data_nascimento date,
    
    criado_em TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

-- RECURSOS --
CREATE TABLE Recurso (
    id SERIAL PRIMARY KEY,
    titulo VARCHAR(255) NOT NULL,
    descricao TEXT,
    privacidade VARCHAR(50) NOT NULL CHECK (privacidade IN ('Publico', 'Privado')) DEFAULT 'Privado',
    autor_id INT NOT NULL REFERENCES "User"(id),
    tipo_recurso VARCHAR(50) NOT NULL CHECK (tipo_recurso IN ('UPLOAD', 'URL', 'NOTA_SIMPLES')),
    visualizacoes INT NOT NULL DEFAULT 0,
    downloads INT NOT NULL DEFAULT 0,
    is_destaque BOOLEAN NOT NULL DEFAULT false,
    
    criado_em TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    atualizado_em TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE RecursoUpload (
    recurso_id INT PRIMARY KEY REFERENCES Recurso(id) ON DELETE CASCADE,
    
    storage_key VARCHAR(1024) NOT NULL, -- O nome/caminho 
    nome_original_arquivo VARCHAR(255) NOT NULL, 
    mime_type VARCHAR(100) NOT NULL, 
    tamanho_arquivo_bytes BIGINT NOT NULL 
);

CREATE TABLE RecursoUrl (
    recurso_id INT PRIMARY KEY REFERENCES Recurso(id) ON DELETE CASCADE,
    url_externa VARCHAR(2048) NOT NULL
);

CREATE TABLE RecursoNota (
    recurso_id INT PRIMARY KEY REFERENCES Recurso(id) ON DELETE CASCADE,
    conteudo_markdown TEXT NOT NULL 
);

-- TAG --
CREATE TABLE Tag ( 
	 id SERIAL PRIMARY KEY, 
	 nome VARCHAR(100) NOT NULL UNIQUE,
);

CREATE TABLE Recurso_Tag ( 
	recurso_id INT NOT NULL REFERENCES Recurso(id) ON DELETE CASCADE, 
	tag_id INT NOT NULL REFERENCES Tag(id) ON DELETE CASCADE, 
	PRIMARY KEY (recurso_id, tag_id) 
);

--playlist--
CREATE TABLE Playlist (
    id SERIAL PRIMARY KEY,
    titulo VARCHAR(255) NOT NULL,  
    descricao TEXT,                 
    autor_id INT NOT NULL REFERENCES "User"(id),
    criado_em TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    atualizado_em TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE Playlist_Recurso (
    playlist_id INT NOT NULL REFERENCES Playlist(id) ON DELETE CASCADE,
    recurso_id INT NOT NULL REFERENCES Recurso(id) ON DELETE CASCADE,
    ordem INT NOT NULL,
    PRIMARY KEY (playlist_id, recurso_id)
);

--LIKE--
CREATE TABLE RecursoLike ( 
	user_id INT NOT NULL REFERENCES "User"(id) ON DELETE CASCADE, 
	recurso_id INT NOT NULL REFERENCES Recurso(id) ON DELETE CASCADE,
	criado_em TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP, 
	PRIMARY KEY (user_id, recurso_id) 
);
```


![](../attachments/Pasted%20image%2020251022184630.png)![](../attachments/Pasted%20image%2020251023185455.png)

### **Visão Geral e Estilo de Design (Design System)**

Projeto: "Acervo Mestre" - Um repositório centralizado de conteúdo pedagógico.

Logo (Obrigatório): O design DEVE usar o logo "Acervo Mestre" fornecido.

Estilo Visual (Crítico): O design deve ser profissional, limpo, minimalista e acadêmico, seguindo o layout do wireframe fornecido (painel lateral esquerdo estático, conteúdo rolável à direita).

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

Fonte: Usar uma fonte Sans-serif clara, moderna e legível (ex: Inter, Roboto, ou Lato).

Hierarquia: Usar pesos de fonte distintos para títulos (Bold), subtítulos (Semibold) e texto corrido (Regular).

---

### **Perfis de Usuário (Define a Visibilidade dos Controles)**

O design deve refletir 4 modos de visualização baseados no perfil:

Gestor (Admin): Vê tudo. Tem acesso ao "Painel de Administração" no menu lateral.

Coordenador (Moderador): Vê tudo (Público/Privado). Vê botões "Adicionar Recurso", "Criar Playlist". Pode "Editar", "Excluir" e "Marcar como Destaque" qualquer recurso.

Professor (Criador): Vê tudo (Público/Privado). Vê botões "Adicionar Recurso", "Criar Playlist". Só pode "Editar" e "Excluir" os seus próprios recursos.

Aluno (Consumidor): Visão mais simples. Vê apenas recursos "Públicos". Não vê botões de admin, edição ou criação. Pode "Curtir" e "Baixar".

---

### **Componente Principal (Resource Card)**

Criar um componente "Card de Recurso" padronizado (bordas arredondadas).

**Conteúdo do Card:**

- Título (em negrito, fonte bold).
    
- Nome do Autor (em cinza claro, fonte menor).
    
- Ícone indicando o tipo (PDF, URL, Nota Simples). e tbm uma img indicando o tipo.
    
- Tags (em formato de "pills").
    
- Métricas (Ícone de olho para visualizações, ícone de download, ícone de coração para curtidas).
    
- Controles no Card (Visíveis no Hover, baseados no perfil):
    
    - Coordenador: Ícone de Estrela (Destaque), Editar, Excluir.
        
    - Professor (se for autor): Editar, Excluir.
        
- Todos: Ícone de "Adicionar à Playlist".
    

---

### **Telas Principais (Wireframes de Alta Fidelidade)**

**A. Tela de Login (RF01)** Conteúdo: Logo "Acervo Mestre" centralizado no topo. Formulário centralizado com campos "E-mail Institucional" e "Senha". Link "Esqueci minha senha".

(Nota: O cadastro é feito pelo Gestor [RF02], então não há link de "Cadastre-se").

**B. Tela Inicial / Dashboard (Layout do Wireframe - Crítico)**

Layout Geral: Um layout de 2 colunas: um Painel de Navegação Estático à esquerda e uma área de conteúdo principal à direita. As seções de conteúdo terão rolagem horizontal.

**Painel Estático (Esquerda):**

- Logo "Acervo Mestre" no topo.
    
- Links de navegação com ícones (ex: Início, Minhas Playlists, Meu Perfil). O ícone ativo deve usar a cor de acento azul.
    
- "Painel de Administração" (visível apenas para Gestor).
    
- Link "Sair" na parte inferior.
    

**Área de Conteúdo (Direita):**

Header da Área: Contém a Barra de Busca (RF15). Placeholder: "Procurar por conteudo".

Filtros (RF16): Abaixo da barra de busca, exibir as opções de filtro ("Matéria", "Formato", "tags") como botões de seleção. O gestor pode mudar as tags

**Seções de Conteúdo (Carrosséis):**

DESTAQUE (RF14): Título da seção. Abaixo, um carrossel de "Cards de Recurso" com scroll horizontal (overflow-x: auto).

MAIS CURTIDOS (RF21): Título da seção. Abaixo, um carrossel de "Cards de Recurso" com scroll horizontal.

RECENTES (RF18): Título da seção. Abaixo, um carrossel de "Cards de Recurso" com scroll horizontal.

Botão de Ação (FAB): (Visível apenas para Professor/Coordenador) Um botão flutuante no canto inferior direito com um ícone de "+" para "Adicionar Recurso" (usar cor de acento azul).

Toda a seção de conteúdo, os três corroseis, devem ser visiveis assim que o usuario entra, sem ter que rolar para baixo.

**C. Página de Detalhes do Recurso (RF17, RF19, RF20)**

Layout: Ao clicar em um card, mostrar esta tela.

Conteúdo:

- Título grande.
    
- Nome do Autor (clicável para "Página do Autor").
    
- Visualizador (Decisão de Requisito):
    
    - Se for "Nota Simples" (RF06) ou "PDF": Exibe o conteúdo renderizado (Markdown) ou um visualizador de PDF embutido.
        
    - Se for "Upload" (DOCX, PPTX) ou "URL" (RF05): Mostra um ícone grande, a descrição e o botão "Baixar Recurso" ou "Acessar Link" (pois a visualização nativa não é suportada, exceto PDF/Nota).
        
- Metadados: Botões "Curtir" (Coração), "Adicionar à Playlist". Métricas (Visualizações, Downloads, Curtidas). Seção de Tags. Descrição completa.
    

**D. Formulário de Adicionar/Editar Recurso (RF04, RF05, RF06, RF07, RF11)**

Layout: Um modal.

Seleção de Tipo (Tabs): "Upload de Arquivo", "Link Externo", "Nota Simples".

Campos Comuns: "Título", "Descrição", "Tags" (campo de seleção/autocomplete com as tags fixas), "Privacidade" (RF07 - Toggle ou Botões de rádio: "Público - Visível para Alunos", "Privado - Apenas Professores/Coord.").

Campos Específicos:

- Tab "Upload": Área de "arrastar e soltar" (dropzone).
    
- Tab "Link Externo": Campo para a "URL".
    
- Tab "Nota Simples": Editor de texto Markdown (react-markdown).
    

Botões: "Salvar Recurso" (com acento azul).

**E. Página do Autor (RF19)**

Layout: Uma página de perfil.

Header: Avatar/Foto do autor, Nome Completo, E-mail Institucional.

Tabs: "Recursos" e "Playlists" (mostrando apenas os itens criados por esse autor).

Conteúdo: Um grid padrão de "Cards de Recurso" ou "Cards de Playlist".

**F. Painel de Administração (Apenas Gestor - RF02, RF03, RF22)**

Layout: Funcional, baseado em tabelas **(seguindo a paleta Light Mode definida)**.

Navegação (Tabs): "Gestão de Usuários", "Gestão de Metadados".

Tab "Gestão de Usuários": Botão "Cadastrar Novo Usuário" (RF02). Tabela de usuários com ações de "Desativar/Ativar" (RF03) e "Editar Perfil".

Tab "Gestão de Metadados" (RF22): Seções para gerenciar as tags fixas (ex: "Matérias", "Séries", "Formatos"). Cada seção deve ter um campo "Adicionar novo..." e uma lista dos itens existentes com botões de "Editar" e "Excluir".


----
### Arquitetura

A arquitetura escolhida foi **MVC com API REST**. Ela deriva do MVC, mas com uma separação física muito mais forte do que no MVC tradicional (onde o backend renderizava o HTML).

Tecnologia escolhida: Node.js para o backend, PostgreSQL para o banco de dados.

- **V (View) = Frontend Desacoplado:**
    - A View será um projeto separado (React) que roda no navegador do usuário.
    - A única responsabilidade do backend é entregar dados puros, não layout.
        
- **C (Controller) = API Endpoints:**
    - Os Controllers (`ResourceController`, `AuthController`) são os **porteiros**.
        
    - Eles "falam" o protocolo HTTP (Recebem `GET/POST`, devolvem Status `200/403/404`).
        
    - **Responsabilidade:** Eles pegam os dados da requisição ( `req.body`), validam se os campos obrigatórios vieram e chamam o método certo do Model. Eles **não** contêm regras de negócio complexas.
        
- **M (Model) = Domínio Rico (Sua Lógica):**
    
    - Aqui está a grande mudança que fizemos nos últimos passos.
        
    - Seus Models (`User`, `Recurso`, `Playlist`) não são apenas espelhos do banco de dados (tabelas). Eles são **Classes Inteligentes**.
        
    - Eles contêm métodos como `verificarSenha()`, `vincularTag()`, `registrarVisualizacao()`.
        
    - **Responsabilidade:** Garantir a integridade dos dados e executar as regras do negócio (ex: "Se é aluno, não pode ver recurso privado").
        

---

### 2. O Fluxo de uma Requisição (Exemplo Prático)

Imagine o cenário: **Um Professor tenta editar um Recurso.**

1. **A View (Frontend):**
    
    - O usuário clica em "Salvar" no navegador.
        
    - O Front envia um JSON para `PUT /api/recursos/50` com os novos dados.
        
2. **O Controller (`ResourceController.update`):**
    
    - Recebe a requisição.
        
    - Identifica quem é o usuário logado (via token).
        
    - Instancia/Busca o objeto `Recurso` (ID 50) do banco.
        
    - **Pergunta crucial:** Ele chama um método de verificação, por exemplo:
        
        JavaScript
        
        ```
        if (!recurso.podeSerEditadoPor(usuarioLogado)) {
             return res.status(403).json({ erro: "Sem permissão" });
        }
        ```
        
    - Se passar, ele atualiza os dados e manda salvar.
        
    - Retorna um JSON `200 OK` com o recurso atualizado.
        
3. **O Model (`Recurso` e `User`):**
    
    - É onde a lógica `podeSerEditadoPor` reside. O Controller não sabe a regra, ele apenas pergunta ao modelo.
        

---

### 3. Por que essa arquitetura é boa para o seu projeto?

1. **Independência de Interface:**
    
    - Como sua API só devolve dados, você pode criar um site hoje e um aplicativo de celular amanhã usando **exatamente o mesmo backend**.
        
2. **Testabilidade:**
    
    - Você pode testar suas regras de negócio (`User.spec.js`, `Recurso.spec.js`) sem precisar subir um servidor, sem banco de dados e sem navegador. É só testar se a lógica da classe funciona.
        
3. **Organização:**
    
    - O Controller fica limpo (fácil de ler as rotas).
        
    - O Model fica rico (toda a regra de negócio do Acervo Mestre está concentrada ali, e não espalhada).
        

Portanto, sim: é um **MVC onde a View foi "expulsa" do servidor** e mora no navegador do cliente, transformando o Controller em uma API de dados.