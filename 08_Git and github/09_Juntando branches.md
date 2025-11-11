

---
### 1. Juntando Branches (git merge)

Na última lição, criamos uma nova _branch_ para trabalhar em um recurso. Agora que o recurso está pronto, queremos trazê-lo de volta para a branch `main`. Esse processo é chamado de **merge** (mesclagem).

O fluxo é o seguinte:

1. **Mude para a branch de destino:** Você deve estar na branch que vai _receber_ as mudanças (geralmente a `main`).
    
    - `git checkout main`
        
2. **Execute o comando de merge:** Chame o `git merge` e diga qual branch você quer "puxar" para dentro da `main`.
    
    - `git merge newFeature` (onde `newFeature` é o nome da sua branch de recurso).
        

**Resultado:** O Git vai pegar todos os commits da sua branch `newFeature` e aplicá-los à branch `main`. Agora, o arquivo `feature1.html` que você criou na outra branch existe também na `main`.

#### 2. Conflitos de Merge (O que fazer quando dá errado) (Páginas 86-90)

Isso é algo que assusta no começo, mas é normal. Um **conflito** acontece quando o Git não sabe como juntar as mudanças automaticamente.

- **Quando acontece?** Geralmente, quando duas pessoas (ou duas branches) modificam a **mesma linha do mesmo arquivo**. O Git não sabe qual versão deve ser mantida.
    
- **O que o Git faz?** Ele para a mesclagem e avisa: `CONFLICT (content): Merge conflict in...`.
    
- **Como resolver?** O Git insere marcadores especiais no arquivo conflitante para mostrar onde está o problema.
    
    - `<<<<<<< HEAD`: O início do código como ele está na sua branch atual (`main`, no exemplo).
        
    - `=======`: Um separador.
        
    - `>>>>>>> conflictDemo`: O fim do código como ele está na branch que você está tentando mesclar (`conflictDemo`, no exemplo).
        
- **Seu trabalho é:**
    
    1. Abrir o arquivo (ex: `feature1.html`).
        
    2. Editar o arquivo manualmente.
        
    3. **Remover todos os marcadores** (`<<<`, `===`, `>>>`).
        
    4. Decidir qual código deve ficar (o seu? o do outro? uma combinação dos dois?).
        
    5. Salvar o arquivo.
        
    6. Fazer um novo commit para finalizar a resolução: `git commit -am "Resolve merge conflict"`.
        

#### 3. Revertendo Mudanças e Corrigindo Commits (Páginas 91-95)

O que fazer se você "commitou" algo errado?

- **Caso 1: Você acabou de fazer o commit e só quer corrigir (ex: esqueceu um arquivo).**
    
    - Use o comando `git commit --amend`.
        
    - Isso permite que você adicione mais mudanças ao seu _último_ commit e até reescreva a mensagem dele.
        
    - **Fluxo:** Faça a correção no código -> rode `git add .` -> rode `git commit --amend`.
        
- **Caso 2: Você quer desfazer o último commit (ou commits).**
    
    - **Atenção:** O livro avisa que o comando `git reset` é **perigoso**, pois ele apaga commits do seu histórico.
        
    - **`git reset --soft HEAD~1`**: Este comando desfaz o último commit, mas **mantém todas as suas alterações de código** na área de _staging_. É útil se você quer "desfazer" o commit para refazê-lo.
        
    - **`git reset --hard HEAD~1`**: Este é o mais perigoso. Ele desfaz o último commit e **apaga permanentemente todas as mudanças de código** daquele commit. Use com extremo cuidado.
        
    - (`HEAD~1` significa "um commit antes do commit atual") .
        
- O livro também menciona `git revert` como outra abordagem, mas não entra em detalhes aqui.