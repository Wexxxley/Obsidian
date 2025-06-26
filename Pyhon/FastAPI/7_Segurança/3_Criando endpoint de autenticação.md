
---

Primeiramente é preciso criar um modelo para nosso token.
![[Pasted image 20250626160514.png]]
- "Bearer" é um tipo de token de acesso que deve ser enviado no cabeçalho Authorization, e basta possuir o token para acessar os recursos protegidos.

Endpoint de login
![[Pasted image 20250626161237.png]] 
- Esse endpoint envia o token para o cliente.
- O **OAuth2PasswordRequestForm** representa um formulário com os campos username e password.
- Quando você usa Depends(), o FastAPI lê esses campos do corpo da requisição (tipo `application/x-www-form-urlencoded`), como esperado pelo padrão OAuth2.

Agora que temos uma forma de autenticar nossos usuários e emitir tokens JWT, é hora de usar essa infraestrutura para proteger nossos endpoints.

Nesse ponto, criaremos uma função `get_current_user` que será responsável por extrair o token JWT do header `Authorization` da requisição, decodificar esse token, extrair as informações do usuário e obter finalmente o usuário do banco de dados. Se qualquer um desses passos falhar, uma exceção será lançada e a requisição será negada. Adicionaremos essa função ao `security.py`: