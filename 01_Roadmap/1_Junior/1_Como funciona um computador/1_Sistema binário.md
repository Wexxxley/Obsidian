
#Concluded 

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

2. No sistema **binário (base 2)** cada "casa" vale 2 vezes mais que a anterior.

![350](../../../attachments/Pasted%20image%2020251027102250.png)

---
### **3. De Bits para Letras**

Computadores não armazenam "letras". Eles armazenam números que representam letras. Para que isso funcione, foi preciso definir um padrão que diz qual número corresponde a qual caractere.

**O Padrão ASCII**: O ASCII foi um dos primeiros padrões criados. Quando você digita a tecla 'H' no seu teclado, o computador armazena o número decimal 72. Quando ele precisa exibir o dado, ele consulta a tabela, vê que 72 significa 'H', e desenha um 'H' na tela.
	![](../../../attachments/Pasted%20image%2020251027102534.png)
- Utiliza 7 bits para representar caracteres, permitindo um total de 128.
- Abrange apenas o alfabeto inglês (sem acentuação), números e alguns caracteres de controle. Ou seja, é insuficiente para idiomas que utilizam acentuação ou alfabetos diferentes 

**Unicode**:  Cada caractere recebe um codigo e cobre todos os sistemas de escrita do mundo, símbolos matemáticos e até emojis. Mas, obviamente consome bem mais espaço.

**UTF-8**: Ele pode usar de 1 a 4 bytes para representar um caractere. Os primeiros 128 caracteres do UTF-8 são idênticos ao ASCII. Isso significa que qualquer arquivo ASCII puro também é um arquivo UTF-8 válido.

Caracteres comuns ocupam apenas 1 byte, enquanto símbolos mais complexos ou emojis ocupam mais espaço.

---
### **4. Byte**

Rapidamente se tornou inconveniente falar de números em sequências longas de bits. A indústria padronizou um agrupamento chamado **Byte**, que é  um conjunto de **8 bits**.
    
- Com 8 bits, você pode criar 256 combinações diferentes (de 0 a 255).
- Isso era mais do que suficiente para cobrir todas as letras (maiúsculas e minúsculas), números e símbolos de pontuação do padrão ASCII. 

![300](../../../attachments/Pasted%20image%2020251027105124.png)