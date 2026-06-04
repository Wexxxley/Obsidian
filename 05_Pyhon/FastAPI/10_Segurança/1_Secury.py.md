
#Concluded 

---
Estude primeiro: [Token JWT](../../../01_Concursos/TI/01_Redes%20de%20computadores/2_Camada%20Aplicação/11_Token%20JWT.md)
Usamos jwt no python com ``pip install pyjwt``

### **1. Funções de hash**
Argon2 é um algorítimo de hash bastante seguro e confiável: ``pip install pwdlib[argon2]``

Criaremos um novo arquivo para gerenciar a segurança: `security.py`.
![Pasted image 20250613141031](../../../attachments/Pasted%20image%2020250613141031.png)
- Foi importado`PasswordHash` que é usada para hashing de senhas.
- `PasswordHash.recommended()`esse comando cria uma instância de `PasswordHash` com configurações recomendadas.

**Hash** é uma função matemática que transforma uma entrada em uma sequência fixa de caracteres.

- **Unidirecional**: não dá para voltar ao valor original.
- **Mesmo input → mesmo output**.
- **Pequena mudança no input → hash totalmente diferente**.
- Impossível descobrir a senha original a partir do hash.

---
### **2. Access Token**

É preciso o `import jwt`
![](../../../attachments/Pasted%20image%2020251210072453.png)
- `create_access_token` é responsável por criar um novo Access Token. Ela recebe um identificador do usuário, adiciona um tempo de expiração ao token. Esses dados, formam o payload. Em seguida, usa a biblioteca `pyjwt` para codificar essas informações em um token.

- `SECRET_KEY` é usada para assinar o token, e o algoritmo `HS256` é usado para a codificação. Em um cenário de produção, você deve manter a `SECRET_KEY` em um local seguro.

![](../../../attachments/Pasted%20image%2020251210072932.png)

---
### **3. Refresh_token**

![](../../../attachments/Pasted%20image%2020251210075113.png)
- **Objetivo:** Gerar um token que permite ao usuário obter novos _Access Tokens_ sem precisar digitar a senha novamente.
- **Tempo de Vida:** Definido por REFRESH_TOKEN_EXPIRE_DAY.
- **Payload:**
    - Subject: O identificador do usuário. 
    - "type": "refresh": Marca este token explicitamente como um token de atualização. Isso impede que um hacker use este token para autenticar diretamente em rotas protegidas.

---
### **4. Decode_token**

![](../../../attachments/Pasted%20image%2020251210075644.png)
- **Objetivo:** Verificar a Integridade e a Validade Temporal do token recebido.
- **Verificação de Assinatura:** A biblioteca pega o _Header_ e o _Payload_ do token recebido, combina com a SECRET_KEY e refaz o cálculo do hash. Se o hash calculado for idêntico ao hash que veio no token, a integridade é confirmada.
- **jwt.ExpiredSignatureError**: O token foi emitido por nós, mas já venceu.
- **jwt.InvalidTokenError**: Cobre qualquer outro erro, como assinatura inválida, formato incorreto e etc.

---
### **5. Create_activation_token**

Nesse sistema, faz sentido o user ativar a sua conta via email.
![](../../../attachments/Pasted%20image%2020251210080339.png)
Este método gera uma credencial de uso único para o fluxo de convite ou recuperação.
