

---
O EditText permite entrad de texto via teclado e possui alguns atributos importantes.

1. **hint**: A dica desaparece quando o usuário começa a digitar. 

2. **inputType:** Este é o atributo mais importante do ponto de vista do sistema. Ele define qual teclado virtual será aberto.
	- `text`: Teclado alfanumérico padrão.
	- `number`: Abre o teclado numérico.
	- `textPassword`: Esconde os caracteres (máscara de senha).
	- `textEmailAddress`: Adiciona o símbolo "@" em destaque no teclado.
	- `phone`: Abre o teclado de discagem telefônica.
	
3. **autoFillHint**: Você indica o que espera e o android faz sugestões ao usuário.

4. **imeOptions**: Define a ação do botão de "Enter" no teclado.
	- `actionNext`: Move o foco para o próximo campo.
	- `actionDone`: Fecha o teclado.
	- `actionSearch`: Mostra uma lupa (ícone de busca).
	![300](../attachments/Pasted%20image%2020260316162644.png)

![](../attachments/Pasted%20image%2020260316163514.png)
![](../attachments/Pasted%20image%2020260316163529.png)

---
### **2. Button**

Buttonn herda todas as propriedades de manipulação de texto, mas vem com comportamentos de interface e estados específicos para cliques.

Além dos atributos comuns (layout_width, layout_height, id), o Button possui propriedades específicas de estado:

- **`android:text`**: Define o rótulo do botão.
    
- **`android:textAllCaps`**: Por padrão, todo o texto do botão fica em maiúsculo.
    
- **`android:backgroundTint`**: Altera a cor de preenchimento do botão sem perder o relevo e as bordas arredondadas padrão. 
    
- **`android:drawableStart` / `android:drawableEnd`**: Permite colocar um ícone dentro do botão, ao lado do texto.    
