
#Concluded 

---
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

### 4. Decode_token

![](../../../attachments/Pasted%20image%2020251210075644.png)

- **Objetivo:** Verificar a **Integridade** e a **Validade Temporal** do token recebido.
    
- **Funcionamento Técnico (`jwt.decode`):**
    
    1. **Verificação de Assinatura:** A biblioteca pega o _Header_ e o _Payload_ do token recebido, combina com a sua `SECRET_KEY` local e refaz o cálculo do hash. Se o hash calculado for idêntico ao hash que veio no token, a integridade é confirmada (ninguém alterou os dados).
        
    2. **Verificação de Algoritmo:** O parâmetro `algorithms=[ALGORITHM]` impede ataques de _downgrade_ (onde um atacante tenta forçar o servidor a aceitar um token sem criptografia).
        
    3. **Verificação de Expiração (`exp`):** A biblioteca compara automaticamente o timestamp atual com o campo `exp` do payload.
        
- **Tratamento de Exceções:**
    
    - `jwt.ExpiredSignatureError`: O token é íntegro (foi emitido por nós), mas já venceu (passou do tempo limite). Retorna `None`.
        
    - `jwt.InvalidTokenError`: Cobre qualquer outro erro, como assinatura inválida (token falsificado/alterado), formato incorreto (não é um JWT) ou decodificação base64 falha. Retorna `None`.


---

### 2. `create_activation_token`

Este método gera uma credencial de **uso único (ou restrito)** para o fluxo de convite ou recuperação.

Python

```
def create_activation_token(email: str) -> str:
    # ...
```

- **Objetivo:** Validar que a pessoa que recebeu o e-mail possui controle sobre aquele endereço.
    
- **Tempo de Vida (`exp`):** Definido por `timedelta(hours=ACTIVATION_TOKEN_EXPIRE_HOURS)`. Geralmente 24h. É um tempo médio: suficiente para o usuário ver o e-mail, mas curto o bastante para não deixar um link de segurança "solto" por aí eternamente.
    
- **Payload (Carga de Dados):**
    
    - `"sub"`: Aqui usamos o **E-mail**, não o ID.
        
        - _Motivo Técnico:_ No fluxo de convite, o usuário pode estar em um estado transitório no banco. Usar o e-mail facilita a busca e validação visual do token se necessário, além de garantir que estamos ativando o e-mail correto.
            
    - `"type": "activation"`: Novamente, a **segregação de função**. Se alguém tentar usar esse token no endpoint `/auth/login` ou `/users/me`, a API rejeitará porque o tipo não é `"access"`.
        

---

        

### Resumo da Segurança

A segurança do seu sistema depende inteiramente da distinção feita nestes payloads:

|**Token**|**Claim type**|**Claim sub**|**Duração Típica**|**Uso Permitido**|
|---|---|---|---|---|
|**Access**|`"access"`|User ID|30 min|Rotas da API (`GET /users`, etc)|
|**Refresh**|`"refresh"`|User ID|7 dias|Apenas endpoint `/auth/refresh`|
|**Activation**|`"activation"`|E-mail|24 horas|Apenas endpoints `/auth/activate`|