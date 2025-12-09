

---

1. **Todos os autenticados**
    
2. **Autor e coordenador e gestor** (Quem criou o item + a moderação)
    
3. **Gestor e coordenador** (Apenas Staff/Administração)
    
4. **Gestor** (Nível máximo)

---
### 1. AuthController

- **POST** `/auth/login`
    - 🔒 **Nível:** Público (Exceção necessária)
    - Recebe e-mail e senha para autenticar o usuário e retornar o Token JWT.
        
- **POST** `/auth/refresh_token`
    - 🔒 **Nível:** Público (Exceção necessária, mas exige token válido)
    - Usado para renovar o token de acesso expirado sem exigir novo login.
    
- **POST** `/auth/forgot_password`
    - 🔒 **Nível:** Público
    - **Lógica:** O usuário informa o e-mail. O sistema verifica se existe. Se existir, envia o link. 
        
- **POST** `/auth/reset_password`
    - 🔒 **Nível:** Público (com Token de validação)
    - **Lógica:** O usuário envia `{ token_do_email, nova_senha }`. O sistema valida o token e altera a senha.
        
- **POST** `/auth/activate_account` (Para o fluxo de convite)
    - 🔒 **Nível:** Público (com Token de ativação)
    - **Lógica:** Endpoint usado quando o usuário clica no e-mail de "Bem-vindo" para definir a primeira senha.
    
- **GET** `/users/me`
	- 🔒 **Nível:** Todos os autenticados
	- Retorna os dados do usuário logado (baseado no token JWT).

**Fluxo de Ativação por E-mail.**

1. **O Cadastro:** O Gestor preenche nome e e-mail. Envia `password: null`
2. **O Backend:**
    - Cria o usuário no banco com status `PENDING` ou `AGUARDANDO_ATIVACAO`.
    - Gera um token único (ex: UUID).
    - Envia um e-mail para o usuário: _"Bem-vindo ao Acervo! Clique aqui para criar sua senha."_
        
3. **A Ação do Usuário:** O usuário clica no link, vai para uma tela de "Definir Senha", preenche e o sistema ativa a conta.
---
### 2. UserController

- **GET** `/users/get/{user_id}`
    - 🔒 **Nível:** Todos os autenticados
    - Retorna os dados de um único usuário pelo ID.
    
- **GET** `/users/get_all/{user_id}`
    - 🔒 **Nível:** Gestor e coordenador
    - Retorna os dados de todos os users.
        
- **POST** `/users/create`
    - 🔒 **Nível:** Gestor e coordenador
    - **Comportamento:**
        - Recebe JSON: `{ nome, email, perfil, password (opcional) }`.
        - Se `password` vier vazio -> Backend gera token de ativação e envia e-mail.
        - Se `avatar` não vier -> Salva como `null`.
    
- **POST** `/users/{id}/avatar`
	- 🔒**Nível:** Dono da conta OU Gestor/Coordenador
	- Para lidar com o upload da imagem separadamente dos dados de texto.
	- Deve permitir setar para vazio.
		
- **PATCH** `/users/patch/{user_id}`
    - 🔒 **Nível:** Autor e coordenador e gestor
    - Atualiza informações cadastrais. _("Autor" aqui é o próprio usuário dono da conta)_.
        
- **DELETE** `/users/delete/{user_id}`
    - 🔒 **Nível:** Gestor
    - Realiza a desativação (soft delete) do usuário.

---
### 3. RecursoController

- **GET** `/recursos/get/{recurso_id}`
    - 🔒 **Nível:** Todos os autenticados
    - Retorna os detalhes de um recurso.
        
- **GET** `/recursos/get_all`
    - 🔒 **Nível:** Todos os autenticados
    - Lista recursos com paginação e filtros.
        
- **GET** `/recursos/download/{recurso_id}`
    - 🔒 **Nível:** Todos os autenticados        
    - Endpoint específico para baixar o arquivo físico.
        
- **POST** `/recursos/create`
    - 🔒 **Nível:** Gestor e coordenador
    - Cria um novo recurso. _(Define que Aluno não pode postar)_.
        
- **PATCH** `/recursos/patch/{recurso_id}`
    - 🔒 **Nível:** Autor e coordenador e gestor
    - Atualiza metadados. O autor edita seu conteúdo; a coordenação modera.
        
- **POST** `/recursos/like/{recurso_id}`
    - 🔒 **Nível:** Todos os autenticados
    - Adiciona uma curtida ao recurso.
        
- **DELETE** `/recursos/delete/{recurso_id}`
    - 🔒 **Nível:** Autor e coordenador e gestor
    - Remove ou despublica o recurso.
        

---
### 4. PlaylistController

- **GET** `/playlists/get/{playlist_id}`
    - 🔒 **Nível:** Todos os autenticados
    - Exibe os detalhes da playlist.
        
- **GET** `/playlists/get_all`
    - 🔒 **Nível:** Todos os autenticados
    - Lista as playlists.
        
- **POST** `/playlists/create`
    - 🔒 **Nível:** Todos os autenticados
    - Cria uma playlist. _(Aqui Alunos podem criar suas listas de estudo)_.
        
- **PATCH** `/playlists/patch/{playlist_id}`
    - 🔒 **Nível:** Autor e coordenador e gestor
    - Atualiza nome/descrição da playlist.
        
- **POST** `/playlists/{playlist_id}/add_resource`
    - 🔒 **Nível:** Autor e coordenador e gestor
    - Adiciona um recurso na playlist.
        
- **DELETE** `/playlists/{playlist_id}/remove_resource/{recurso_id}`
    - 🔒 **Nível:** Autor e coordenador e gestor
    - Remove um recurso da playlist.
        
- **DELETE** `/playlists/delete/{playlist_id}`
    - 🔒 **Nível:** Autor e coordenador e gestor
    - Exclui a playlist inteira.
        
- **POST** `/playlists/like/{playlist_id}`
    - 🔒 **Nível:** Todos os autenticados
    - Adiciona uma curtida à playlist.

---
### 5. TagController

- **GET** `/tags/get_all`
    - 🔒 **Nível:** Todos os autenticados
    - Retorna tags para o autocomplete.
        
- **POST** `/tags/create`
    - 🔒 **Nível:** Gestor e coordenador
    - Cria uma nova tag.
        
- **DELETE** `/tags/delete/{id}`
    - 🔒 **Nível:** Gestor
    - Remove uma tag.
        
