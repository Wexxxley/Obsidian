

---
A ferramenta toast fornece feedbacks rápidos e não intrusivos ao usuário. O Toast aparece como um pequeno pop-up que não interrompe a interação com a tela e desaparece automaticamente após alguns segundos.

- **Exemplos:** "E-mail enviado", "Download concluído" ou "Item salvo nos favoritos".

Para criar um Toast, utiliza-se o método estático makeText. Ele exige três parâmetros obrigatórios:
- **Context:** Define em qual parte da aplicação o Toast está operando. 
- **Text:** A String que será exibida para o usuário.
- **Duration:** Define por quanto tempo a mensagem ficará na tela. 
    - Toast.LENGTH_SHORT: Exibição por cerca de 2 segundos.
    - Toast.LENGTH_LONG: Exibição por cerca de 3.5 segundos.

![500](../../attachments/Pasted%20image%2020260320084924.png)
![300](../../attachments/toast.gif)



---
### **2. Snackbar**

Snackbar é um componente de interface do Android que fornece mensagens informativas na parte inferior da tela, permitindo interações rápidas através de botões de ação. Diferente do Toast, o Snackbar pode ser fechado pelo usuário e pode conter uma ação (como "Desfazer" ou "Ver"). 

Para exibir um Snackbar, o Compose utiliza quatro elementos trabalhando em conjunto:
- **Scaffold:** O layout mestre que define a estrutura visual.
- **SnackbarHost:** O componente responsável por "hospedar" a mensagem, controlando onde ela aparece e as animações.
- **SnackbarHostState:** O objeto que gerencia o estado.
- **CoroutineScope:** Necessário porque a função de exibir o Snackbar é "suspensa" (executada de forma assíncrona).

Ao disparar a mensagem através do `snackbarHostState.showSnackbar()`, podemos configurar:

- **message:** O texto principal da mensagem.
    
- **actionLabel:** O texto do botão de ação (ex: "OK", "Desfazer").
    
- **withDismissAction:** Um booleano que, se `true`, adiciona um ícone "X" para fechar a mensagem manualmente.
    
- **duration:** Define o tempo de exibição:
    
    - `Short` / `Long`: Desaparece automaticamente.
        
    - `Indefinite`: Permanece na tela até que o usuário interaja.
        
## 4. Customização Visual

A aula também demonstra que é possível personalizar as cores do Snackbar dentro do parâmetro `snackbarHost` do `Scaffold`. Utiliza-se o componente `Snackbar` e suas propriedades:

- **containerColor:** Altera a cor de fundo (ex: `Color.Red`).
    
- **contentColor:** Altera a cor do texto da mensagem.
    
- **actionColor:** Altera a cor do texto do botão de ação.
    
- **dismissActionContentColor:** Altera a cor do ícone de fechar (X).
    

## 5. Resumo de Diferenças: Toast vs Snackbar

- **Posição:** O Toast costuma ser centralizado ou flutuante; o Snackbar é fixado na base (Material Design).
    
- **Interação:** O Toast é apenas informativo; o Snackbar permite botões de ação e fechamento manual.
    
- **Fila:** O `SnackbarHostState` garante que apenas um Snackbar apareça por vez, colocando os outros em uma fila de espera automaticamente.
    

Deseja que eu explique como integrar o Snackbar com um **Floating Action Button (FAB)** para que o botão suba automaticamente quando a mensagem aparecer?