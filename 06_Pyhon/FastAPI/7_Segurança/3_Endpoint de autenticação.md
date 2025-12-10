
---
### **1. Criando endpoint de login**

Primeiramente é preciso criar um modelos para nossos tokens.
![](../../../attachments/Pasted%20image%2020251210073401.png)

**Endpoint de login**
![](../../../attachments/Pasted%20image%2020251210073458.png) 

---
### **2. Get_current_user**

Nesse ponto, criaremos uma função `get_current_user` que será responsável por extrair o token do header `Authorization`, decodificar esse token, extrair as informações do usuário e obter finalmente o usuário do banco de dados. 
![](../../../attachments/Pasted%20image%2020251210073900.png)
- O protocolo HTTP é stateless. O servidor não "lembra" quem fez a requisição anterior. Portanto, cada requisição precisa provar sua identidade e autorização isoladamente.
- A função `get_current_user` resolve isso executando quatro validações críticas de segurança em tempo de execução
- Se tudo for válido, ela retorna uma instância do modelo ORM (User). Isso evita que você tenha que consultar o banco de dados manualmente em cada rota. O objeto retornado já está pronto para uso.

**Endpoint de teste**
![](../../../attachments/Pasted%20image%2020251210074518.png)
No FastAPI, a execução do get_current_user ocorre através do sistema de Injeção de Dependência.

1. O servidor recebe a requisição HTTP.
2. Antes de executar a função da rota, o FastAPI detecta o parâmetro `Depends(get_current_user)` e executa e dependência.
3. Se houver sucesso o objeto `User` retornado é passado como argumento para a função da rota. A função `get_me` é finalmente executada, recebendo o objeto `current_user` já validado.
