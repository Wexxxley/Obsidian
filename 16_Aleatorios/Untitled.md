
Com certeza. Aqui está a lista dos endpoints organizada por Controller, seguindo o padrão que você estabeleceu no `UserController` e mapeada com os requisitos do documento "Acervo Mestre".

### 1. AuthController

Responsável pela autenticação e segurança do sistema.

- **POST** `/auth/login`: Recebe e-mail e senha para autenticar o usuário e retornar o Token JWT1.
    
- **POST** `/auth/refresh_token`: (Opcional) Usado para renovar o token de acesso expirado sem exigir novo login.
    

---

### 2. UserController

Responsável pelo gerenciamento de usuários (Professores, Coordenadores, Alunos e Gestores)2.

- **GET** `/users/get/{user_id}`: Retorna os dados de um único usuário pelo ID.
    
- **GET** `/users/get_all`: Lista todos os usuários com suporte a paginação e filtro por status (ativo/inativo).
    
- **POST** `/users/create`: Cadastra um novo usuário no sistema3.
    
- **PATCH** `/users/patch/{user_id}`: Atualiza informações cadastrais do usuário.
    
- **DELETE** `/users/delete/{user_id}`: Realiza a desativação (soft delete) do usuário4.
    

---

### 3. RecursoController

Este é o principal controller do sistema, lidando com os materiais pedagógicos, uploads e interações.

- **GET** `/recursos/get/{recurso_id}`: Retorna os detalhes de um recurso, incluindo autor e contagem de visualizações5555555.
    
- **GET** `/recursos/get_all`: Lista recursos com paginação. Aceita parâmetros para busca por texto 6, filtros (Matéria, Formato) 7e ordenação por recentes8.
    
- **GET** `/recursos/download/{recurso_id}`: Endpoint específico para baixar o arquivo físico (se for upload). Incrementa o contador de downloads9999.
    
- **POST** `/recursos/create`: Cria um novo recurso. Deve suportar cadastro de Arquivo (Upload) 10, Link Externo 11ou Nota Simples12. Também define as Tags 13e Privacidade14.
    
- **PATCH** `/recursos/patch/{recurso_id}`: Atualiza metadados. Permite ao autor editar 15, ao coordenador moderar 1616e marcar como destaque17.
    
- **POST** `/recursos/like/{recurso_id}`: Adiciona uma curtida ao recurso18.
    
- **DELETE** `/recursos/delete/{recurso_id}`: Remove ou despublica o recurso do sistema19191919.
    

---

### 4. PlaylistController

Responsável pela organização de recursos em sequências de aulas.

- **GET** `/playlists/get/{playlist_id}`: Exibe os detalhes da playlist e a lista de recursos contidos nela.
    
- **GET** `/playlists/get_all`: Lista as playlists do usuário logado ou públicas.
    
- **POST** `/playlists/create`: Cria uma nova playlist vazia com título e descrição20.
    
- **PATCH** `/playlists/patch/{playlist_id}`: Atualiza nome, descrição ou reordena os itens da playlist21.
    
- **POST** `/playlists/{playlist_id}/add_resource`: Adiciona um recurso existente dentro de uma playlist22.
    
- **DELETE** `/playlists/{playlist_id}/remove_resource/{recurso_id}`: Remove um recurso específico de dentro da playlist.
    
- **DELETE** `/playlists/delete/{playlist_id}`: Exclui a playlist inteira.
    
- **POST** `/playlists/like/{playlist_id}`: (Opcional) Adiciona uma curtida à playlist23.
    

---

### 5. TagController

Auxilia na categorização e busca de conteúdos.

- **GET** `/tags/get_all`: Retorna todas as tags cadastradas para alimentar o "Autocomplete" no front-end24.
    
- **POST** `/tags/create`: Cria uma nova tag manualmente (caso não seja criada automaticamente no fluxo de recurso).
    

---

### 6. MetadadosController

Responsável pela padronização do sistema, acessível apenas ao Gestor.

- **GET** `/metadados/get_all`: Retorna as listas de valores permitidos para "Matérias", "Séries" e "Formatos" para os filtros e cadastros25.
    
- **POST** `/metadados/create`: Adiciona uma nova opção de metadado (ex: nova disciplina).
    
- **DELETE** `/metadados/delete/{id}`: Remove uma opção de metadado, com validação de uso.