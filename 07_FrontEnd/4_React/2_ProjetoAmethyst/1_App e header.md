
#Concluded 

---
![](../../../attachments/Pasted%20image%2020251127080555.png)
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
![](../../../attachments/Pasted%20image%2020251127075548.png)

**Props:**
1. **isLoggedIn**: Define se mostra o botão "Entrar" ou o Avatar do usuário.
2. **currentScreen**: Se for video, mostra o botão "Exportar Transcrição".
3. **onLoginClick**: É um callback handler. Quando clicada, avisa ao App para mudar o estado showLoginModal para true.
4. **onLogoClick:** Callback para resetar a tela para home.    
    
![](../../../attachments/Pasted%20image%2020251127075635.png)
