

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

