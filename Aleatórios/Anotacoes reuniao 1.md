
- User(id, nome, email, senha_hash, perfil, status(ativo/inativo), data_nasc)
- No momento de cadastro o user recebe um email para definir sua senha.

- Para os arquivos teriamos uma tabrla com metadados dos arquivos. E o armazenamento real ficaria por conta do MinIO.
- MinIO. O MinIO é um **serviço de armazenamento de objetos auto-hospedado (self-hosted)**. Pense nele como se você pudesse rodar a sua própria "Amazon S3" no seu próprio servidor.

```sql

CREATE TABLE "User" (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE,
    senha_hash VARCHAR(255) NOT NULL,
    
    perfil VARCHAR(50) NOT NULL CHECK (perfil IN ('Gestor', 'Coordenador', 'Professor', 'Aluno')),
    status VARCHAR(50) NOT NULL CHECK (status IN ('Ativo', 'Inativo')) DEFAULT 'Ativo',
    data_nascimento date
    
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
```


- Para o markdown no front **(react-markdown)**.  O ecossistema de plugins do react-markdown (especialmente o remark-gfm para GFM - GitHub Flavored Markdown e o uso com react-syntax-highlighter para código) facilitará muito a renderização desses elementos de forma bonita e funcional.

- **Padrao de Arquitetura MVC (Model-View-Controller):** É um padrão de arquitetura que separa a aplicação em três componentes principais: Modelo (dados e lógica de negócio), Visão (interface do usuário/Frontend) e Controlador (recebe requisições e coordena Modelo e Visão)."
- model/ controller/ routes/ server.js app.js
- **DTO** (Data Transfer Object),"É um padrão de design (ou objeto) usado para transferir dados entre as camadas da aplicação. 

- tags fixas e _padronizados_ ("Matéria",  "Formato"). 

- Ao clicar em um recurso o user tem a possibilidade de criar ou adicionar a uma playlist. 


- Tem que ter a possibilidade de marcar e desmarcar como destaque um recurso ()