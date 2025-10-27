


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

![350](attachments/Pasted%20image%2020251027102250.png)

---
### **3. De Bits para Letras)**

Computadores não armazenam "letras". Eles armazenam números que _representam_ letras. Para que isso funcione, foi preciso definir um padrão que diz qual número corresponde a qual caractere.

**O Padrão ASCII (American Standard Code for Information Interchange)**: O ASCII foi um dos primeiros padrões criados para isso. Quando você digita a tecla 'H' no seu teclado, o computador não armazena um 'H'. Ele armazena o número decimal **72**. Quando ele precisa exibir esse dado, ele consulta a tabela ASCII, vê que 72 significa 'H', e desenha um 'H' na tela.
	![](attachments/Pasted%20image%2020251027102534.png)
- Cada número era representado por 7 bits

Em vez de usar apenas os códigos de 0 a 127, o UNICODE utiliza códigos de valor bem maiores. Com isso, pode representar **todos os caracteres específicos** de diversos idiomas. Novos códigos são regularmente atribuídos para novos caracteres, como caracteres latinos (acentuados ou não), gregos, cirílicos, armênios, hebraicos, tailandeses, hiraganas, katakanas etc. Só o alfabeto chinês Kanji contém 6.879 caracteres. Assim sendo, o UNICODE define uma correspondência entre símbolos e números.
---
### **Byte**

Rapidamente se tornou inconveniente falar de números em sequências longas de bits. A indústria padronizou um agrupamento chamado **Byte**, que é simplesmente um conjunto de **8 bits**.
    
- Com 8 bits, você pode criar 256 combinações diferentes (de 0 a 255).
    
- Isso era mais do que suficiente para cobrir todas as letras (maiúsculas e minúsculas), números e símbolos de pontuação do padrão ASCII. Por isso, por muito tempo, 1 caractere = 1 byte.
    

**Subtópico 2.3: A Limitação do ASCII e a Solução: Unicode (e Emojis!)**

- **O Problema:** O ASCII (e seus 256 lugares) funcionava bem para o inglês, mas e as outras línguas? E os acentos (como 'ç' ou 'ã'), os caracteres asiáticos (como '猫') ou os símbolos matemáticos (como 'π')? Não havia espaço.
    
- **A Solução:** O **Unicode** foi criado. É um padrão muito maior que o ASCII (na verdade, o ASCII é uma pequena parte dele). O Unicode tem o objetivo de atribuir um número único para _cada caractere em cada idioma do mundo_.
    
- **Emojis:** Os emojis que usamos todos os dias são, na verdade, caracteres Unicode. O computador armazena um número (como `U+1F600`) e seu celular ou computador sabe que deve desenhar um 😀 (rosto sorridente) na tela.