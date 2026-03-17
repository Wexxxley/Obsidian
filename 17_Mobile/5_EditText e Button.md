

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

---

## 2. Tratamento de Eventos (Ouvintes)

Existem duas formas principais de capturar o clique do usuário:

#### A. Via XML (`android:onClick`) - Menos Recomendada

Você define o nome de uma função no XML e a implementa na sua `MainActivity`.

- **XML:** `android:onClick="enviarDados"`
    
- **Código:** `fun enviarDados(view: View) { ... }`
    
- _Desvantagem:_ Menos seguro para refatoração e difícil de testar.
    

#### B. Via Programação (`OnClickListener`) - Padrão da Indústria

Você busca a referência do botão pelo ID e anexa um "ouvinte".

Kotlin

```
val btnEnviar = findViewById<Button>(R.id.btn_enviar)

btnEnviar.setOnClickListener {
    // Lógica executada ao clicar
    println("Botão clicado!")
}
```

---

## 3. Estados do Botão (StateListDrawable)

Um botão não é apenas uma imagem estática. Ele reage ao toque. O Android gerencia isso através de uma lista de estados (State List).

- **Pressed:** Quando o usuário está com o dedo sobre o botão.
    
- **Focused:** Quando o botão é selecionado via teclado ou D-pad (importante para acessibilidade).
    
- **Disabled:** Quando `enabled="false"`.
    

Se você quiser criar um botão totalmente customizado (ex: um botão redondo), você precisará criar um arquivo em `res/drawable` que defina o comportamento para cada um desses estados.

---

## 4. Tipos Modernos de Botões (Material Design)

Com a biblioteca Material Components (que você provavelmente tem no seu `build.gradle`), você tem acesso a variações estilizadas:

1. **Contained Button:** Botão com preenchimento total (para ações primárias).
    
2. **Outlined Button:** Apenas a borda (para ações secundárias).
    
3. **Text Button:** Sem borda ou fundo (para ações de menor importância, como "Cancelar").
    
4. **Floating Action Button (FAB):** O botão circular flutuante (comum para "Adicionar").
    

---