


---

Tudo, absolutamente tudo que um computador faz, desde mostrar este texto até rodar um jogo complexo, é baseado em um conceito muito simples: o **sistema binário**.

### **1. Conceitos fundamentais**

**Definição**: <mark style="background: #ADCCFFA6;">Sistema binário é um sistema de numeração que usa apenas dois dígitos: 0 e 1. Cada um desses dígitos é chamado de "bit".</mark>

**Por que os computadores usam:** Para um computador, é muito mais fácil e confiável representar coisas usando apenas dois estados. No hardware, isso se traduz em:    
- **0:** Ausência de corrente elétrica.
- **1:** Presença de corrente elétrica.

É muito <mark style="background: #ADCCFFA6;">mais simples para uma máquina gerenciar bilhões desses pequenos "interruptores" (transistores) do que tentar entender 10 níveis diferentes de voltagem</mark> (como seria necessário para o sistema decimal de 0 a 9).

---

### **2. Binário e o sistema Decimal**

1. No sistema **decimal (base 10)** cada "casa" de um número vale 10 vezes mais que a anterior.
	- O número **123  = (1 x 100) + (2 x 10) + (3 x 1)**

2. No sistema **binário (base 2)** mas cada "casa" vale 2 vezes mais que a anterior.

**Subtópico 1.3: Como contar em binário (usando o exemplo das lâmpadas)**

O vídeo usa lâmpadas para ilustrar isso perfeitamente. Imagine 3 lâmpadas (3 bits):

- **Lâmpada 1 (direita):** Representa a casa do **1**.
    
- **Lâmpada 2 (meio):** Representa a casa do **2**.
    
- **Lâmpada 3 (esquerda):** Representa a casa do **4**.
    

(Note que as casas são potências de 2: $2^0=1$, $2^1=2$, $2^2=4$, depois 8, 16, 32, etc.)

Agora, vamos contar:

- **Decimal 0:** `(Apagada) (Apagada) (Apagada)` -> `0 0 0`
    
- **Decimal 1:** `(Apagada) (Apagada) (Acesa)` -> `0 0 1` (Porque a casa do 1 está ligada)
    
- **Decimal 2:** `(Apagada) (Acesa) (Apagada)` -> `0 1 0` (Porque a casa do 2 está ligada)
    
- **Decimal 3:** `(Apagada) (Acesa) (Acesa)` -> `0 1 1` (Porque 2 + 1 = 3)
    
- **Decimal 4:** `(Acesa) (Apagada) (Apagada)` -> `1 0 0` (Porque a casa do 4 está ligada)
    
- **...e assim por diante até 7:** `(Acesa) (Acesa) (Acesa)` -> `1 1 1` (Porque 4 + 2 + 1 = 7)
    

Com apenas 3 bits (lâmpadas), podemos representar 8 números diferentes (de 0 a 7). Com mais bits, podemos representar números muito maiores.

---

Quando quiser, pode digitar `next` para irmos ao Tópico 2, onde veremos como esses números viram letras e dados úteis.