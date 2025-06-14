
---

Foi alterado security.py
![[Pasted image 20250614155912.png]]
- Foram adicionados contantes: tempo de expiração do token, algoritimo de criptografia usado e a chave secreta.
- O método create_access_token cria o token jwt.

Foi criado o rota para auth.
![[Pasted image 20250614160142.png]]
- Esse endpoint envia o token para o cliente.
- O `OAuth2PasswordRequestForm` é um modelo **padrão do OAuth2** que:
    - Espera os **dados do formulário** com `username` (que será usado como `email`) e `password`.
    - Ele não lida com JSON, mas sim `x-www-form-urlencoded`, como é padrão em OAuth2.