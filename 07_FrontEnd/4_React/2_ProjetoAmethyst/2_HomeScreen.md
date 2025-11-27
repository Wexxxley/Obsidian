
#Concluded 

---
![](../../../attachments/Pasted%20image%2020251127080627.png)
### **1. App**

Voltando ao arquivo App.jsx, após o cabeçalho, temos a área principal de conteúdo.
![](../../../attachments/Pasted%20image%2020251127080132.png)
O React verifica se a variável de estado screen é igual a home. Se for, ele renderiza o componente HomeScreen. 
    
**Props passadas:** 
1. **isLoggedIn**: Para a tela saber se bloqueia ou libera o botão de processar.
2. **isLoading**: Para mostrar o feedback visual.
3. **onProcessVideo**: A função que a tela deve chamar quando o usuário apertar o botão.

---
### **2. HomeScreen.**

**Estado Interno**
![](../../../attachments/Pasted%20image%2020251127080408.png)
A URL sendo digitada só interessa a este componente. 

No input, vemos isso:
![](../../../attachments/Pasted%20image%2020251127081607.png)
- Isso é chamado de **Componente Controlado**. O que aparece na tela não é o que o navegador guarda, mas sim o que está na variável `url`. Cada tecla pressionada dispara `setUrl`, que atualiza o estado e redesenha o input com a nova letra. [7_Componentes controlados](../1_Fundamentos/7_Componentes%20controlados.md)

- **disabled={isLoading}**: garante que o input esteja desativado enquanto está processando.

![](../../../attachments/Pasted%20image%2020251127081259.png)
- **Lifting State:** O componente filho HomeScreen não processa o vídeo. Ele chama a função onProcessVideo e entrega a URL para o pai. [6_Callback handlers e lifting state](../1_Fundamentos/6_Callback%20handlers%20e%20lifting%20state.md)

![](../../../attachments/Pasted%20image%2020251127081819.png)

---

### 3. **handleProcessVideo**

Quando o botão é clicado na HomeScreen, esta função no App.jsx é disparada:
![](../../../attachments/Pasted%20image%2020251127082401.png)

1. **setIsLoading(true)** 
2. **Assíncrono:** O navegador faz a requisição para o seu servidor local.
3. **Atualização de Estado (`setVideoData` e `setScreen`):**
    - Ao receber os dados, o `App` guarda tudo em videoData.
    - Muda `screen` para video.
