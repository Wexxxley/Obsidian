
---
### **1. Criando endpoint para logar**

Primeiramente é preciso criar um modelo para nosso token.
![[Pasted image 20250626160514.png]]
- "Bearer" é um tipo de token de acesso que deve ser enviado no cabeçalho Authorization, e basta possuir o token para acessar os recursos protegidos.

Endpoint de login
![[Pasted image 20250626161237.png]] 
- Esse endpoint envia o token para o cliente.
- O **OAuth2PasswordRequestForm** representa um formulário com os campos username e password.
- Quando você usa Depends(), o FastAPI lê esses campos do corpo da requisição (tipo `application/x-www-form-urlencoded`), como esperado pelo padrão OAuth2.

---
### **2. Proteção de endpoint**
Agora que temos uma forma de autenticar nossos usuários e emitir tokens JWT, é hora de usar essa infraestrutura para proteger nossos endpoints.

Nesse ponto, criaremos uma função `get_current_user` que será responsável por extrair o token  do header `Authorization`, decodificar esse token, extrair as informações do usuário e obter finalmente o usuário do banco de dados. 
![[Pasted image 20250627131312.png]]
- **token:** Injeta o token JWT extraído do cabeçalho Authorization.
- **credentials_exception:** Prepara uma exceção padrão para lançar caso a autenticação falhe.
- **Tenta decodificar** o token JWT usando a chave secreta e o algoritmo.
- Se tudo deu certo, retorna o usuário autenticado.

Finalmente protegendo uma rota.
![[Pasted image 20250626163831.png]]

