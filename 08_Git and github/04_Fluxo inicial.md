
#Concluded 

---
### **1. Inicializando um Projeto (git init)**

1. Primeiro, você cria uma pasta para o seu projeto e entra nela.
    - `mkdir novo-projeto`
    - `cd novo-projeto`
        
2. Dentro da pasta, você executa o comando git init. Esse comando "inicializa" um repositório Git vazio. Ele cria a pasta oculta `.git` .
    - `git init`
        

---
### **2. Adicionando Mudanças (git add)** 

Para dizer ao Git "comece a rastrear este arquivo" usamos o `git add`. Este processo é chamado de **Staging**.

- Para adicionar um arquivo específico:
    - `git add README.md`
        
- Para adicionar múltiplos arquivos de uma vez: 
	- `git add arquivo1.html arquivo2.css`.
        
- Para adicionar TODOS os arquivos modificados no diretório atual :
    - `git add .`

---
### **3. Salvando as Mudanças (git commit)** 

Um commit cria um checkpoint permanente do seu projeto. Você só faz o commit das mudanças que estão na área de staging.

 - `git commit -m "Sua mensagem de commit aqui"`

