
---
### **1. Criando endpoint de login**

Primeiramente é preciso criar um modelos para nossos tokens.
![](../../../attachments/Pasted%20image%2020251210073401.png)

**Endpoint de login**
![](../../../attachments/Pasted%20image%2020251210073458.png) 

---
### **2. Proteção de endpoint**

Agora que temos uma forma de autenticar nossos usuários e emitir tokens JWT, é hora de usar essa infraestrutura para proteger nossos endpoints.

Nesse ponto, criaremos uma função `get_current_user` que será responsável por extrair o token  do header `Authorization`, decodificar esse token, extrair as informações do usuário e obter finalmente o usuário do banco de dados. 

![](../../../attachments/Pasted%20image%2020251210073900.png)
- O protocolo HTTP é stateless. O servidor não "lembra" quem fez a requisição anterior. Portanto, cada requisição precisa provar sua identidade e autorização isoladamente.
- A função `get_current_user` resolve isso executando quatro validações críticas de segurança em tempo de execução
- Se tudo for válido, ela retorna uma instância do modelo ORM (User). Isso evita que você tenha que consultar o banco de dados manualmente em cada rota. O objeto retornado já está pronto para uso.

![](../../../attachments/Pasted%20image%2020251210074518.png)
No FastAPI, a execução do get_current_user ocorre através do sistema de Injeção de Dependência.

1. O servidor recebe a requisição HTTP.
2. Antes de executar a função da rota, o FastAPI detecta o parâmetro `Depends(get_current_user)` e executa e dependência.
3. 
    - O `security = HTTPBearer()` extrai o valor do cabeçalho `Authorization`.
        
    - A função `get_current_user` é executada.
        
    - **Se houver exceção (`raise HTTPException`):** O ciclo é interrompido imediatamente. O FastAPI retorna o erro JSON para o cliente e a função da rota **nunca é executada**.
        
    - **Se houver sucesso:** O objeto `User` retornado é passado como argumento para a função da rota.
        
4. **Execução da Rota:** A função `get_me` é finalmente executada, recebendo o objeto `current_user` já validado e populado.
    

### Diagrama de Sequência Simplificado

Snippet de código

```
Client ->> FastAPI: GET /users/me (Header: Bearer eyJhb...)
FastAPI ->> HTTPBearer: Extrai token do Header
HTTPBearer -->> FastAPI: Token String
FastAPI ->> get_current_user: Executa validação
get_current_user ->> PyJWT: Decodifica e verifica assinatura
PyJWT -->> get_current_user: Payload (Claims)
get_current_user ->> Database: SELECT * FROM user WHERE id = sub
Database -->> get_current_user: Objeto User
get_current_user -->> FastAPI: Objeto User validado
FastAPI ->> Rota (get_me): Executa passando (current_user)
Rota (get_me) -->> Client: Retorna JSON 200 OK
```