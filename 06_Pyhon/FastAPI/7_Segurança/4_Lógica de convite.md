
#Concluded 

---
Estes dois endpoints implementam juntos o Fluxo de Convite de Usuário. O Gestor cria o registro, e o Usuário termina definindo sua própria senha.
### **1. Create_user**

![](../../../attachments/Pasted%20image%2020251210080846.png)
- Este endpoint é usado pelo Gestor. A função dele é colocar o usuário no sistema.
- **Fluxo 1:** Se o gestor já digitar uma senha, o usuário é criado imediatamente como Ativo. 
- **Fluxo 2:** Se o gestor não digitar senha:
    1. O sistema salva o usuário como `AguardandoAtivacao` e com senha `None`.
    2. O sistema gera um Token de Ativação (um JWT especial que dura 24h).
    3. O sistema usa `background_tasks` para enviar esse token por e-mail.

---
### **2. Activate_account**

![](../../../attachments/Pasted%20image%2020251210080717.png)

- Este endpoint é usado pelo Usuário Convidado. A função dele é validar se o convite é verdadeiro e permitir que o usuário defina sua senha.
-  **O Token é autêntico?**  Verifica se o token foi gerado pelo seu servidor e se não expirou.
- **O Token é do tipo certo?** Impede que alguém use um _Access Token_ roubado para tentar mudar a senha de outra pessoa. 
- **O Usuário existe?** Busca o usuário pelo e-mail do token
- **O Usuário já foi ativado?** Impede que o usuário clique no link duas vezes ou que um hacker tente resetar a senha de um usuário que já está usando o sistema.    
