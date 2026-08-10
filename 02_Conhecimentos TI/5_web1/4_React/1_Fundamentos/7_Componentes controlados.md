
#Concluded 

---
Elementos de formulário HTML (como `<input>`, `<textarea>`, `<select>`) mantêm nativamente seu próprio estado interno no DOM. Quando você digita em um campo de texto, o navegador atualiza o valor visualmente, independentemente do React.

O componente `Search` é um **Uncontrolled Component**. O React recebe os eventos de mudança (`onChange`), mas não determina explicitamente o que está sendo exibido no input.

**Controlled Components**: Para resolver isso, devemos converter o input em um Componente Controlado. Isso significa que o React se torna a "**única fonte da verdade**". 

No `App`, passamos o valor atual de `searchTerm` como uma prop para o `Search`. 
![](../../../../attachments/Pasted%20image%2020251124135453.png)

No `Search`, atribuímos essa prop ao atributo `value` do elemento HTML `<input>`.
![](../../../../attachments/Pasted%20image%2020251124135514.png)

Ao adotar esse padrão, garantimos que o estado visual (DOM) e o estado lógico (React) estejam sempre perfeitamente sincronizados.
