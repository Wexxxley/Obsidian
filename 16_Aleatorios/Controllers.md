

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

---
### 2. UserController

- **GET** `/users/get/{user_id}`
    - 🔒 **Nível:** Todos os autenticados
    - Retorna os dados de um único usuário pelo ID.
    
- **GET** `/users/get_all/{user_id}`
    - 🔒 **Nível:** Todos os autenticados
    - Retorna os dados de todos os users.
        
- **POST** `/users/create`
    - 🔒 **Nível:** Gestor e coordenador
    - Cadastra um novo usuário no sistema.
    
- **POST** `/users/{id}/avatar`
	- 🔒**Nível:** Dono da conta. 
	- Para lidar com o upload da imagem separadamente dos dados de texto.
	- Deve permitir setar para vazio.
	
- **POST** `/auth/forgot_password`
	- Envia e-mail com link de recuperação.
    
- **POST** `/auth/reset_password`: Recebe o token do e-mail e a nova senha.
		
- **PATCH** `/users/patch/{user_id}`
    - 🔒 **Nível:** Autor e coordenador e gestor
    - Atualiza informações cadastrais. _("Autor" aqui é o próprio usuário dono da conta)_.
        
- **DELETE** `/users/delete/{user_id}`
    - 🔒 **Nível:** Gestor
    - Realiza a desativação (soft delete) do usuário.

    

**2. Recuperação de Senha**


    
    - _Por que:_ Usuários sempre esquecem senhas.

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
        

---

### 6. Extras Recomendados (Respondendo sua dúvida)

Sim, para o sistema ficar completo, recomendo fortemente adicionar estes 3 endpoints:

- **GET** `/users/me`
    
    - 🔒 **Nível:** Todos os autenticados
        
    - **Por que é necessário:** O front-end usa isso logo após o login para saber "quem sou eu", pegar o avatar e o ID do usuário sem precisar decodificar o token manualmente ou passar ID na URL.
        
- **GET** `/dashboard/stats`
    
    - 🔒 **Nível:** Gestor e coordenador
        
    - **Por que é necessário:** Retorna números gerais (Total de Usuários, Total de Downloads, Recursos Novos) para a tela inicial do painel administrativo.
        
- **POST** `/auth/reset_password`
    
    - 🔒 **Nível:** Público
        
    - **Por que é necessário:** Endpoint para redefinir a senha caso o usuário esqueça ("Esqueci minha senha").
---

