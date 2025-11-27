

---
### **Parte 1: O Container Principal (App.jsx) e o Cabeçalho**

O arquivo `App.jsx` atua como o **Orquestrador de Estado**. Ele não tem muita lógica visual complexa, mas gerencia _quem_ está logado, _qual_ tela deve aparecer e _quais_ modais estão abertos.

#### **1. Análise do `App.jsx` (Início)**

**Imports:**

- `useState`, `useEffect`: Hooks fundamentais para gerenciar memória do componente e ciclo de vida.
    
- Importação dos componentes filhos (`Header`, `HomeScreen`, etc.).
    

Estados (useState):

Aqui definimos a "verdade única" da aplicação.

1. `const [screen, setScreen] = React.useState('home');`
    
    - **Função:** Roteamento manual. Como não estamos usando `react-router`, essa string define o que o usuário vê.
        
    - **Valores:** `'home'` (tela inicial) ou `'video'` (tela do player).
        
2. `const [user, setUser] = React.useState(null);`
    
    - **Função:** Armazena o objeto do usuário logado `{ id, name, email, hasApiKey }`.
        
    - **Técnica:** Se for `null`, a aplicação entende como "deslogado".
        
3. `const [videoData, setVideoData] = React.useState(null);`
    
    - **Função:** Armazena o JSON pesado que vem do backend (legendas sincronizadas, ID do vídeo, título). É passado para a `VideoScreen`.
        
4. `const [isLoading, setIsLoading] = React.useState(false);`
    
    - **Função:** Feedback visual. Bloqueia a interface enquanto o backend processa o vídeo.
        
5. `const [showLoginModal, setShowLoginModal] = React.useState(false);` e `[showApiKeyModal, ...]`
    
    - **Função:** Booleanos simples para controlar a visibilidade dos modais (pop-ups). O React renderiza condicionalmente com base nisso.
        

**Efeitos (`useEffect`):**

JavaScript

```
React.useEffect(() => {
  const savedUser = localStorage.getItem('amethyst_user');
  if (savedUser) {
      setUser(JSON.parse(savedUser));
  }
}, []);
```

- **Objetivo:** Persistência de Sessão.
    
- **Funcionamento:** O array de dependências vazio `[]` garante que isso rode **apenas uma vez** quando o `App` é montado (ao atualizar a página). Ele verifica se há um usuário salvo no navegador (`localStorage`) para evitar que o usuário tenha que logar toda vez que der F5.
    

---

#### **2. Renderização e o Componente `Header`**

Agora entramos no `return (...)` do `App.jsx`. O primeiro componente encontrado é o `<Header />`.

JavaScript

```
<Header 
  isLoggedIn={!!user}
  user={user} 
  currentScreen={screen} 
  onLoginClick={() => setShowLoginModal(true)} 
  onLogoClick={() => setScreen('home')}
  onLogout={handleLogout}
  onOpenApiKeyModal={() => setShowApiKeyModal(true)}
/>
```

Vamos pausar o `App.jsx` e entrar no arquivo `Header.jsx`.

---

### **Componente: Header.jsx**

Este é um **Componente de Apresentação** (Dumb Component). Ele recebe dados e funções do pai e apenas mostra coisas na tela. Ele não tem `state` próprio complexo.

**Props (Parâmetros recebidos):**

1. `isLoggedIn`: Booleano (convertido de `!!user` no App). Define se mostra o botão "Entrar" ou o Avatar do usuário.
    
2. `currentScreen`: String. Usada para renderização condicional. Se for `'video'`, ele mostra o botão extra "Exportar Transcrição".
    
3. `onLoginClick`: Função de callback. Quando clicada, avisa ao `App.js` para mudar o estado `showLoginModal` para `true`.
    
4. `onLogoClick`: Callback para resetar a tela para `'home'`.
    

**Lógica Interna:**

- **Renderização Condicional Ternária:**
    
    JavaScript
    
    ```
    {!isLoggedIn ? ( ...Botão Entrar... ) : ( ...Avatar e Ações... )}
    ```
    
    Isso é clássico do React. O componente muda drasticamente sua aparência baseado apenas em uma prop.
    
- **Interatividade:** O `Header` não sabe _como_ fazer login. Ele apenas dispara o evento `onClick={onLoginClick}`, delegando a responsabilidade de volta para o `App.jsx`.
    

---

**Resumo até aqui:** O `App` inicializou seus estados e montou o cabeçalho. O cabeçalho sabe se o usuário está logado e, se o usuário clicar em "Entrar", ele chama a função do pai para abrir o modal.

Quando estiver pronto para ver a **HomeScreen** e como os dados fluem para o processamento de vídeo, diga **"next"**.