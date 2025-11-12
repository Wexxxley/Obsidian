

---
### **1. Rebaseando Commits (git rebase)** 

O Rebase é uma alternativa ao `git merge`. Enquanto o merge junta duas linhas do tempo e cria um "commit de merge", o `rebase` reescreve o histórico.

O `rebase` pega todos os commits da sua branch atual e os move para o topo de outra branch. Isso faz com que seu histórico pareça uma linha reta e limpa.

**Exemplo: Atualizando sua Branch de Recurso**

1. Você está trabalhando na sua `feature-branch`.    
2. Enquanto isso, novos commits são adicionados à branch `dev` por outros colegas.
3. Sua `feature-branch` agora está desatualizada. Você quer trazer essas novas mudanças da `dev` para a sua branch.
4. Estando na sua `feature-branch`, você roda: `git rebase dev`.
5. O Git vai "levantar" seus commits, aplicar os novos commits da `dev` e, em seguida, reaplicar os _seus_ commits, um por um, no topo.

