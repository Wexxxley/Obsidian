

#Concluded 

---

O objetivo técnico aqui é extrair a lógica de persistência de estado (sincronização com `localStorage`) do componente `App` para uma função reutilizável. 

### 1. Criação do Hook useStorageState

Movemos o useState e o useEffect para fora do App e para dentro da nova função useStorageState.
![](../../attachments/Pasted%20image%2020251124144440.png)
- **Parâmetros Genéricos:** O hook aceita `key` e `initialState` como argumentos, tornando-o agnóstico ao domínio (não sabe o que é "search", apenas sabe o que é uma chave e um valor).
    
- **Array de Dependências:** Note que `key` foi adicionado ao array de dependências `[value, key]`. Isso é crucial: se a chave de armazenamento mudar durante a vida útil do componente, o efeito deve rodar novamente para salvar os dados no local correto 1.

---
### **2. Integração** 

Agora, o componente `App` consome este novo hook da mesma maneira que consumia o `useState`, mas passando a chave de armazenamento desejada.
![](../../attachments/Pasted%20image%2020251124144328.png)

O componente App não conhece mais os detalhes de implementação do localStorage. Ele apenas sabe que possui um estado que é persistido (useStorageState). Se decidirmos mudar de localStorage para sessionStorage ou cookie no futuro, alteraremos apenas o hook, e todos os componentes que o utilizam serão atualizados automaticamente.
