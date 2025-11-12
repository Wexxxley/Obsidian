

---
### **1. Salvando Mudanças Temporárias (git stash)

Imagine que você está no meio da implementação de um novo recurso, com vários arquivos modificados. De repente, você precisa trocar de branch para corrigir um bug urgente. Você não pode fazer commit das suas mudanças (porque elas estão incompletas), mas o Git não deixa você trocar de branch com o "trabalho sujo".
    
**Solução:** O comando `git stash` guarda temporariamente todas as suas modificações locais, revertendo seu projeto ao estado do último commit. Depois de rodar `git stash`, seu `git status` mostrará que o projeto está "limpo", permitindo que você troque de branch.

**Restaurando suas mudanças:** Existem duas formas principais de pegar suas mudanças de volta:
- **`git stash apply`**: Aplica as mudanças que você guardou de volta, mas mantém uma cópia delas em uma pilha para o caso de você querer aplicá-las em outro lugar.
    
- **`git stash pop`**: A diferença é que remove as mudanças da pilha depois de aplicá-las.
