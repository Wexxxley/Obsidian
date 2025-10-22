
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
![](attachments/Pasted%20image%2020251022165352.png)

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


![](attachments/Pasted%20image%2020251022184630.png)