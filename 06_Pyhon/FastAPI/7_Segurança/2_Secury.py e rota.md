
#Concluded 

---
Argon2 é um algorítimo de hash bastante seguro e confiável: ``pip install pwdlib[argon2]``

Criaremos um novo arquivo para gerenciar a segurança: `security.py`.
![Pasted image 20250613141031](../../../attachments/Pasted%20image%2020250613141031.png)
- Foi importado`PasswordHash` que é usada para hashing de senhas.
- `PasswordHash.recommended()`esse comando cria uma instância de `PasswordHash` com configurações recomendadas.

É preciso o `import jwt`
![](../../../attachments/Pasted%20image%2020251210072453.png)
- `create_access_token` é responsável por criar um novo Access Token. Ela recebe um identificador do usuário, adiciona um tempo de expiração ao token. Esses dados, formam o payload. Em seguida, usa a biblioteca `pyjwt` para codificar essas informações em um token.

- `SECRET_KEY` é usada para assinar o token, e o algoritmo `HS256` é usado para a codificação. Em um cenário de produção, você deve manter a `SECRET_KEY` em um local seguro.

![](../../../attachments/Pasted%20image%2020251210072932.png)

---
### **Sobre hash**
Hash é uma função matemática que transforma uma entrada em uma sequência fixa de caracteres.

- **Unidirecional**: não dá para voltar ao valor original.
- **Mesmo input → mesmo output**.
- **Pequena mudança no input → hash totalmente diferente**.
- Impossível descobrir a senha original a partir do hash.
