
#Concluded 

---
### **1. Configuração Inicial do Git (git config)**

Antes de começar a usar o Git, você precisa fazer uma configuração inicial. O Git armazena essas informações em todos os _commits_ que você faz.

1. **Configurar come de esuário:** Nome que aparecerá como autor dos seus commits.    
    - `git config --global user.name "Seu Nome"` 
        
2. **Configurar seu Email:**
    - `git config --global user.email "seuemail@exemplo.com"`
        
3. **Configurar nome da Branch Padrão:** Este comando garante que seus novos repositórios locais usem "main" por padrão.
    - `git config --global init.defaultBranch main`

>[!note]
> `--global` é uma flag que diz ao Git para usar essas configs para todos os projetos no seu pc.
> 
> As configurações globais são salvas em um arquivo chamado `.gitconfig` na sua pasta de usuário (home).

- **Para ver sua configuração:** Você pode listar todas as configurações aplicadas com o comando `git config --list`.
    ![](../attachments/Pasted%20image%2020251111153203.png)


---
### **2. Diretório .git**

Quando você transforma uma pasta em um repositório Git, o Git cria uma pasta oculta chamada `.git`. É dentro desta pasta que o Git armazena todo o histórico, configurações e tudo o que ele precisa para rastrear seu projeto.
