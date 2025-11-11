
#Concluded 

---
### 1. Git Branches

Até agora, trabalhamos apenas na branch `main`. Esta é a branch principal do projeto.

**Mas o que é uma branch?** A analogia mais fácil é a de uma árvore: você tem o tronco principal (`main`) e pode criar novos galhos (`branches`) que saem dele.
        
**Por que usar branches?**
- Para **isolar o desenvolvimento**.
- Quando você quer criar um novo recurso ou corrigir um bug (ex: "consertar formulário de contato"), você **cria uma nova branch**.
- Você faz todo o seu trabalho e seus commits _dentro dessa nova branch_, sem afetar ou bagunçar a branch `main`, que deve conter apenas o código estável e funcionando.
- Isso permite que vários desenvolvedores trabalhem em recursos diferentes ao mesmo tempo, cada um em sua própria branch.
- Quando o recurso está pronto e testado, você "junta" (mescla) sua branch de volta à `main`.

![](../attachments/Pasted%20image%2020251111161906.png)

---
### 2. Comandos Essenciais para Branches

- **Listar todas as branches:** Ele listará todas as branches locais. A branch em que você está atualmente terá um asterisco (`*`) ao lado.
    - `git branch`
        
- **Criar uma nova branch:**    
    - `git branch nome-da-nova-branch`
        
- **Mudar para outra branch:**
    - `git checkout nome-da-branch`
        
- **Deletar uma branch (localmente):**  Você não pode deletar a branch em que está.
    - `git branch -d nome-da-branch`
        
- **Renomear uma branch:**
    - `git branch -m nome-antigo nome-novo`