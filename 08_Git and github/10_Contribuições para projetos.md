

---
### **1. Clonando um Repositório (git clone)**

Na maioria das vezes, você não vai começar um projeto do zero. Você vai se juntar a um projeto que já existe. O git clone é o comando que você usa para baixar uma cópia completa de um repositório do GitHub para o seu computador.

1. No GitHub, vá até a página do repositório.
2. Clique no botão verde "Code".
3. Copie a URL.
4. No seu terminal, navegue até a pasta onde você quer salvar o projeto e rode:
	`git clone git@github.com:usuario/nome-do-repo.git`


---
### **2. Fork**

Aqui está um cenário comum: você quer contribuir para um projeto de código aberto, mas você não tem permissão para fazer `git push` diretamente para ele. 

- Um Fork é o ato de criar uma cópia exata de um repositório de outra pessoa, mas sob a sua própria conta do GitHub.
- Agora você tem uma "versão sua" do projeto e pode fazer `push` para ela à vontade.

---
### 3. O Fluxo Completo de Contribuição

1. **Clone ou Inicie:** `git clone` um projeto existente ou `git init` um novo.
    
2. **Crie uma Branch:** **Sempre** crie uma nova branch para seu trabalho com `git checkout -b nome-da-branch`.
    
3. **Trabalhe:** Faça suas mudanças no código.
    
4. **Salve Localmente:** Use `git add .` e `git commit -m "mensagem"`.
    
5. **Envie para o Remoto:** `git push origin nome-da-branch`.
    
6. **Abra um Pull Request (PR):** Peça para suas mudanças serem mescladas na branch `main`.
    
7. **Revise:** Alguém vai revisar seu código e, se estiver tudo certo, vai aprová-lo e mesclá-lo.    

---
### 4. Pull Request

Um Pull Request é a forma de dizer no GitHub: "Eu fiz mudanças nesta branch e gostaria que vocês as puxassem e mesclassem na branch principal". É a versão "online" do comando `git merge`.


1. **Faça o Fork** do repositório original (se não for seu).
    
2. **Clone o _seu_ fork** para o seu computador (`git clone ...`).
    
3. **Crie uma nova branch** (`git checkout -b meu-recurso`).
    
4. **Faça seu trabalho** (edite arquivos, `add`, `commit`).
    
5. **Envie sua branch** para o _seu_ fork no GitHub (`git push origin meu-recurso`).
    
6. **Vá ao GitHub:** Vá para a página do seu fork (ou a do original; o GitHub geralmente mostra um aviso).
    
7. **Clique em "Pull Requests"** e depois em "New pull request".
    
8. **Configure o PR:**
    
9. **Escreva** um título e uma descrição claros para o seu PR.

