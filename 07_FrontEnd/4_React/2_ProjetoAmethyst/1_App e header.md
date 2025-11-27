


---
### **1. App.jsx estados e efeitos**

App é o orquestrador de estados e componentes.

**Estados:**
![](../../../attachments/Pasted%20image%2020251127073006.png)
1.  **screen**: Essa string define o que o usuário vê. home, video.
        
2. **user:** Armazena o objeto do usuário logado { id, name, email, hasApiKey }. Se for null, a aplicação entende como "deslogado".
        
3. **videoData**: Armazena o JSON pesado que vem do backend (legendas, ID do vídeo, título). 
        
4. **isLoading**: Feedback visual. Bloqueia a interface enquanto há processamento.
        
5. **showLoginModal e showApiKeyModal:** Booleanos simples para controlar a visibilidade dos modais. 

**Efeitos:**
![](../../../attachments/Pasted%20image%2020251127073447.png)
 - O array de dependências vazio garante que isso rode **apenas uma vez** quando o App é montado. Ele verifica se há um usuário salvo no navegador (localStorage) para evitar que o usuário tenha que logar toda vez que o user atualizar a página.

---
### **2. Componente Header**

Agora entramos no return  do App. O primeiro componente encontrado é o Header.
![](../../../attachments/Pasted%20image%2020251127073740.png)

Header recebe dados e funções do pai e apenas mostra coisas na tela. Ele não tem state próprio complexo.

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