

---
### 1. Inicializando um Projeto (git init)

1. Primeiro, você cria uma pasta para o seu projeto e entra nela.
    - `mkdir novo-projeto`
    - `cd novo-projeto`
        
2. Dentro da pasta, você executa o comando:
    - `git init`
        

- Esse comando "inicializa" um repositório Git vazio. Ele cria a pasta oculta `.git` . É nesta pasta que o Git vai salvar todo o histórico de mudanças.

---
### 2. Verificando o Status (git status)

- Se você rodar `git status` em um projeto novo, ele dirá:
    - `On branch main`
    - `No commits yet` 
        
- Crie um arquivo
- Se você rodar `git status` de novo, a saída muda:
    - Ele agora mostra: `Untracked files:` (Arquivos não rastreados)
    - E lista o `README.md`.

---
### 3. Adicionando Mudanças (git add) 

Para dizer ao Git "comece a rastrear este arquivo" usamos o `git add`. Este processo é chamado de **"Staging"**.

- Para adicionar um arquivo específico:
    - `git add README.md`
        
- Para adicionar múltiplos arquivos de uma vez: 
	- `git add arquivo1.html arquivo2.css`.
        
- Para adicionar **TODOS** os arquivos modificados no diretório atual :
    - `git add .`

---
### 4. Salvando as Mudanças (git commit) 

Um "commit" cria um ponto de salvamento (checkpoint) permanente do seu projeto. Você só faz o _commit_ das mudanças que estão na área de _staging_.

- O comando básico para fazer um commit é:
    - `git commit -m "Sua mensagem de commit aqui"`


---
### 5. Vendo as Diferenças (git diff)

O comando `git diff` é usado para mostrar as diferenças exatas no conteúdo dos arquivos que foram alterados, mas que **ainda não foram para a área de staging** (você ainda não usou `git add`).

- **O que ele mostra?** 13
    
    - **Linhas removidas:** Começam com um sinal de menos (`-`).
        
    - **Linhas adicionadas:** Começam com um sinal de mais (`+`)14.
        
- No exemplo do livro, adicionar a linha "Git is awesome" ao `README.md` mostra a nova linha com um `+` na frente15151515.
    

É uma prática excelente **sempre** rodar `git status` e `git diff` antes de fazer um `git add` e `git commit`, para ter certeza de que você está salvando exatamente as mudanças que deseja16.

**Variações do `git diff`:**

O livro menciona duas outras variações úteis17171717:

- `git diff --staged` (ou `git diff --cached`): Mostra as diferenças dos arquivos que você **já adicionou** ao _staging area_ (depois de rodar `git add`), comparando-os com o último commit.
    
- `git diff HEAD`: Mostra todas as mudanças nos arquivos rastreados desde o último commit, independentemente de estarem ou não no _staging_.
    

---

Agora sabemos como iniciar um projeto, salvar mudanças e, o mais importante, inspecionar _exatamente_ o que mudou.

Quando estiver pronto para as **páginas 50-62** (que cobrem como ver o histórico com `git log` e como ignorar arquivos com `.gitignore`), me diga **next**.