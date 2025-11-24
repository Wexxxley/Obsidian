

---
Atualmente, se você atualizar a página, o termo de busca e o estado da aplicação são resetados. O objetivo é persistir o `searchTerm` no **localStorage** do navegador para que a última busca seja lembrada.

O hook `useEffect` permite executar efeitos após o React renderizar o componente.

**Sincronizar Estado com LocalStorage**
![](../../attachments/Pasted%20image%2020251124142359.png)
- **Função de efeito:** A função passada para o `useEffect` é executada após o **componente ser montado** e após cada **atualização**.

- **Array de dependencias:** Ao passar `[searchTerm]`, instruímos o React a executar o efeito **apenas se** a variável `searchTerm` tiver mudado. Se o array estivesse vazio `[]`, o efeito rodaria apenas uma vez na montagem . 

- **State:** Precisamos que o estado inicial do `useState` não seja fixo, mas sim o que estiver salvo no armazenamento.
