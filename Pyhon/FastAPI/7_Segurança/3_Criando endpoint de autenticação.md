
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

Nesse ponto, criaremos uma função `get_current_user` que será responsável por extrair o token JWT do header `Authorization` da requisição, decodificar esse token, extrair as informações do usuário e obter finalmente o usuário do banco de dados. 
![[Pasted image 20250626162924.png]]
- **token:** Injeta o token JWT extraído do cabeçalho Authorization (usando o esquema Bearer).

---

```python
    credentials_exception = HTTPException(  
        status_code=HTTPStatus.UNAUTHORIZED,
        detail='Could not validate credentials',
        headers={'WWW-Authenticate': 'Bearer'},
    )
```
- Prepara uma exceção padrão para lançar caso a autenticação falhe.

---

```python
    try:
        payload = decode(token, SECRET_KEY, algorithms=[ALGORITHM])
        subject_username = payload.get('sub')

        if not subject_username:
            raise credentials_exception  
```
- **Tenta decodificar** o token JWT usando a chave secreta e o algoritmo.
- **Extrai o campo `sub`** (subject), que normalmente é o username do usuário.
- Se não houver `sub`, lança exceção de credenciais inválidas.

---

```python
    except DecodeError:
        raise credentials_exception  
```
- Se o token não puder ser decodificado (token inválido, expirado, etc.), lança exceção de credenciais inválidas.

---

```python
    user = session.exec(select(User).where(User.username == subject_username))
   
    if not user:
        raise credentials_exception  
```
- Busca o usuário no banco de dados pelo username extraído do token.
- Se não encontrar, lança exceção de credenciais inválidas.

---

```python
    return user
```
- Se tudo deu certo, retorna o usuário autenticado.

---

**Resumo:**  
A função valida o token JWT, extrai o usuário, busca no banco e retorna o usuário autenticado. Se qualquer etapa falhar, retorna erro 401 (não autorizado).