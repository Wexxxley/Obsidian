

---
Atualmente, se você atualizar a página, o termo de busca e o estado da aplicação são resetados. O objetivo é persistir o `searchTerm` no **localStorage** do navegador para que a última busca seja lembrada.

O hook `useEffect` permite executar efeitos após o React renderizar o componente.

**Sincronizar Estado com LocalStorage**: Sempre que o `searchTerm` mudar, queremos salvar esse valor.
![](../../attachments/Pasted%20image%2020251124141942.png)
- **Função de efeito:** A função passada para o `useEffect` é executada após o **componente ser montado** e após cada **atualização**.

- **Array de dependencias:** Ao passar `[searchTerm]`, instruímos o React a executar o efeito **apenas se** a variável `searchTerm` tiver mudado. Se o array estivesse vazio `[]`, o efeito rodaria apenas uma vez na montagem . 

**Inicializar Estado com LocalStorage**: Agora precisamos que o estado inicial do `useState` não seja fixo ('React'), mas sim o que estiver salvo no armazenamento.

JavaScript

```jsx
const App = () => {
  // Inicialização Lazy (Preguiçosa) / Condicional
  // Tenta ler do localStorage; se não existir (null), usa 'React' como fallback.
  const [searchTerm, setSearchTerm] = React.useState(
    localStorage.getItem('search') || 'React'
  );

  React.useEffect(() => {
    localStorage.setItem('search', searchTerm);
  }, [searchTerm]);
  
  // ...
```

**Fluxo de Dados Completo:**

1. **Mount (Montagem):** O `useState` lê o localStorage. Se houver "Redux" salvo, `searchTerm` inicia como "Redux".
    
2. **Render:** O componente exibe "Redux" no input.
    
3. **Effect:** O `useEffect` roda. Ele salva "Redux" no localStorage (sobrescrevendo o que já estava lá, o que é uma operação idempotente segura).
    
4. **Update (Atualização):** O usuário digita "J".
    
5. **Render:** O componente re-renderiza com `searchTerm` igual a "J".
    
6. **Effect:** O React compara a dependência `searchTerm` ("J") com a anterior ("Redux"). Como mudou, ele executa o efeito novamente, salvando "J" no localStorage.
    

Essa combinação garante que o estado do React e o armazenamento do navegador estejam sempre sincronizados.