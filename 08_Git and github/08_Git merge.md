
#Concluded 

---
### **1. Juntando Branches (git merge)**

Na última lição, criamos uma nova branch para trabalhar em um recurso. Agora que o recurso está pronto, queremos trazê-lo de volta para a branch `main`.  O fluxo é:

1. **Mude para a branch de destino:** 
    - `git checkout main`
        
2. **Execute o comando:** Execute `git merge` e diga qual branch você quer "puxar" para dentro da `main`.
    - `git merge newFeature`

---
### **2. Conflitos de Merge**

Um conflito acontece quando o Git não sabe como juntar as mudanças automaticamente. Geralmente, quando duas pessoas (ou duas branches) modificam a mesma linha do mesmo arquivo. O Git não sabe qual versão deve ser mantida.

**Como resolver?** O Git insere marcadores especiais no arquivo conflitante para mostrar onde está o problema.
    
    - <<<<<<< HEAD: O início do código como ele está na sua branch atual
        
    - =======`: Um separador.
        
    - `>>>>>>> conflictDemo`: O fim do código como ele está na branch que você está tentando mesclar (`conflictDemo`, no exemplo).
        
- **Seu trabalho é:**
    1. Abrir o arquivo (ex: `feature1.html`).
    2. Editar o arquivo manualmente.
    3. **Remover todos os marcadores** (`<<<`, `===`, `>>>`).
    4. Decidir qual código deve ficar (o seu? o do outro? uma combinação dos dois?).
    5. Salvar o arquivo.
    6. Fazer um novo commit para finalizar a resolução: `git commit -am "Resolve merge conflict"`.

---
#### 3. Revertendo Mudanças e Corrigindo Commits 

O que fazer se você "commitou" algo errado?

- **Caso 1: Você acabou de fazer o commit e só quer corrigir.
    - Use o comando `git commit --amend`.
    - Isso permite que você adicione mais mudanças ao seu _último_ commit e até reescreva a mensagem dele.
    - **Fluxo:** Faça a correção no código -> rode `git add .` -> rode `git commit --amend`.
        
- **Caso 2: Você quer desfazer o último commit.**

    - **`git reset --soft HEAD~1`**: Este comando desfaz o último commit, mas **mantém todas as suas alterações de código** na área de _staging_. É útil se você quer "desfazer" o commit para refazê-lo.
    - **`git reset --hard HEAD~1`**: Este é o mais perigoso. Ele desfaz o último commit e **apaga permanentemente todas as mudanças de código** daquele commit. 
    - (`HEAD~1` significa "um commit antes do commit atual") .
