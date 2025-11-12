
#Concluded 

---
### **1. Enviando mudanças (Git push)**

Agora que você tem um repositório local com commits, é hora de enviar seu trabalho.

**1. Crie um Repositório Remoto (GitHub)**

- Primeiro, você precisa ir ao site do GitHub e criar um novo repositório. Não adicione um README, crie-o como um repositório vazio.

**2. Linkando seu Repositório Local ao Remoto**

- O GitHub lhe dará a URL (HTTPS ou SSH) do seu repositório.    
- No seu terminal, dentro da pasta do seu projeto, use o comando:
	`git remote add origin git@github.com:seu_usuario/seu_repo.git`

**3. Enviando os Commits (git push)**

- Este é o comando que pega seus commits locais e os envia para o repositório remoto.
     `git push -u origin main`    

---
### **2. Baixando Mudanças (git pull)** 

O que acontece quando outra pessoa (ou você mesmo, de outro computador) envia mudanças para o repositório remoto? Seu repositório local fica desatualizado.

- O `git pull` é o comando usado para **buscar e baixar as mudanças** do repositório remoto e **automaticamente mesclá-las** ao seu repositório local.`git pull origin main`
    
- Se você tentar fazer `git push` de novas mudanças, mas o seu repositório local estiver desatualizado, o Git irá rejeitar seu push .
    
- Sempre execute `git pull` para obter as últimas mudanças _antes_ de tentar fazer `git push` das suas próprias mudanças.    

