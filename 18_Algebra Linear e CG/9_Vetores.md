

---
### **1. Vetor**

Geometricamente, um vetor é uma **seta** que possui três características fundamentais:
- **Módulo/Magnitude:** O "tamanho" da seta.
- **Direção**
- **Sentido:** Para onde a ponta da seta aponta.

Diferente de um ponto (que é apenas uma localização), o vetor representa um deslocamento ou uma força.

**Duas dimensões $R²$**
![400](../attachments/Pasted%20image%2020260309084811.png)

**Três dimensões $R³$**
![400](../attachments/Pasted%20image%2020260309084918.png)

**Vetores opostos** são vetores mesma direção, mesmo módulo mas com sentidos diferentes.
$a = (1,2,3)$ e $b = (-1,-2,-3)$
![400](../attachments/Pasted%20image%2020260309085909.png)

---
### 2. **Soma de vetores**
![](../attachments/Pasted%20image%2020260312135419.png)

---
### 3. Produto escalar

O resultado é um **número único**. Ele mede o quanto um vetor "projeta" sobre o outro ou o quanto eles apontam para a mesma direção.

- **A Fórmula:** $\vec{a} \cdot \vec{b} = |\vec{a}| |\vec{b}| \cos(\theta)$
    
- **Em coordenadas:** $(a_1 \cdot b_1) + (a_2 \cdot b_2) + (a_3 \cdot b_3)$

![500](../attachments/20260310_080016587.jpg)

O valor do produto escalar revela a relação angular entre os vetores:

- **Positivo** $0^\circ \leq \theta < 90^\circ$. Ângulo agudo.
- **Zero** $\theta = 90^\circ$ Ortogonais/perpendiculares.
- **Negativo** $90^\circ < \theta \leq 180^\circ$ ângulo obtuso

---
### 4. Produto Vetorial

O resultado é um **novo vetor**. Esse novo vetor é especial porque ele é **perpendicular (90°)** aos dois vetores originais ao mesmo tempo. É exclusivo do espaço 3D.

- **A Fórmula:** $|\vec{a} \times \vec{b}| = |\vec{a}| |\vec{b}| \sin(\theta)$
    
- **Direção:** Segue a "Regra da Mão Direita".

Vamos usar os vetores:
- $\vec{A} = (3, 4, 0)$
- $\vec{B} = (1, -2, 0)$
![](../attachments/20260315_091949672.jpg)
---
### **5. Multiplicação por um escalar**

Se $k = 3$ e $\vec{v} = (1, -2, 4)$:
$$3 \cdot \vec{v} = (3 \times 1, 3 \times -2, 3 \times 4) = (3, -6, 12)$$

Quando você multiplica um vetor por um escalar, o efeito visual depende do valor de $k$:
- **Se $k > 1$:** O vetor mantém a direção, mas aumenta o comprimento.
- **Se $0 < k < 1$:** O vetor mantém a direção, mas diminui o comprimento.
- **Se $k = -1$:** O vetor mantém o tamanho, mas inverte o sentido.
- **Se $k = 0$:** O vetor vira o vetor nulo.

---
### **6. Módulo de um vetor**

O módulo/normade um vetor é o seu comprimento ou magnitude. Representamos o módulo de um vetor $\vec{v}$ como $\|\vec{v}\|$ ou $|\vec{v}|$.

A lógica para calcular o tamanho de um vetor é a mesma do Teorema de Pitágoras. Se você tem um vetor no espaço 3D $\vec{v} = (x, y, z)$, o módulo é a raiz quadrada da soma dos quadrados de suas componentes:
$$\|\vec{v}\| = \sqrt{x^2 + y^2 + z^2}$$

Se você tem um vetor $\vec{v} = (3, -4, 0)$:
$$\|\vec{v}\| = \sqrt{3^2 + (-4)^2 + 0^2}$$
$$\|\vec{v}\| = \sqrt{9 + 16 + 0} = \sqrt{25} = 5$$


---
### **7. Normalização**

Normalizar um vetor significa transformá-lo em um **vetor unitário**, ou seja, um vetor que mantém a mesma direção e sentido do original, mas cujo módulo é exatamente 1.

![](../attachments/20260312_140505068.jpg)

---
### **8. Projeção escalar e vetorial**

A **projeção escalar** representa o **comprimento** da sombra de $\vec{u}$ sobre a direção de $\vec{v}$.
$$Proj_{\vec{v}}\vec{u} = \frac{\vec{u} \cdot \vec{v}}{|\vec{v}|}$$

A **projeção vetorial** é um vetor. É a sombra propriamente dita, com direção e sentido. Ela pega o comprimento (projeção escalar) e o transforma em um vetor que "mora" em cima da linha de $\vec{v}$
$$proj_{\vec{v}}\vec{u} = \left( \frac{\vec{u} \cdot \vec{v}}{|\vec{v}|^2} \right) \vec{v}$$    
![](../attachments/20260315_090053500.jpg)


---

- **Ponto - Ponto = Vetor** (Distância e direção entre dois lugares).
    
- **Ponto + Vetor = Ponto** (Você está em um lugar e se desloca para outro).
    
- **Vetor + Vetor = Vetor** (Dois deslocamentos seguidos resultam em um deslocamento final).

Na Geometria Analítica e na Computação Gráfica, o termo **"Normal"** não tem nada a ver com ser "comum". Ele é um conceito puramente geométrico de **orientação**.

## 1. O que é um Vetor Normal?

Dizemos que um vetor é **Normal** a uma superfície (como um plano, um triângulo ou o polígono de um personagem) quando ele é **perpendicular** a essa superfície.

- **Em 2D:** A normal é um vetor que forma **90°** com uma reta.
    
- **Em 3D:** A normal é um vetor que forma **90°** com todos os vetores contidos em um plano.
    

Imagine uma mesa: o vetor normal é uma caneta em pé sobre ela. Não importa para onde você gire a caneta (desde que ela continue em pé), ela estará apontando na direção "Normal" da mesa.

---

## 2. O que significa "Encontrar a Normal"?

Encontrar a normal significa descobrir para qual direção uma face está "olhando". Na computação, as superfícies são feitas de triângulos. Para o computador saber qual é a "frente" e qual é a "costa" desse triângulo, ele calcula a normal.

**Como se calcula?**

Como vimos no exercício anterior, se você tem três pontos ($p_0, p_1, p_2$):

1. Cria dois vetores: $\vec{A} = (p_1 - p_0)$ e $\vec{B} = (p_2 - p_0)$.
    
2. Faz o **Produto Vetorial**: $\vec{n} = \vec{A} \times \vec{B}$.
    
3. O resultado $\vec{n}$ é a **Normal**.
    

---

## 3. Por que isso é vital para você (Dev)?

Se você está criando um sistema ou um jogo no seu Linux Mint, a Normal serve para:

- **Iluminação (Shading):** O computador calcula o ângulo entre o "Vetor da Luz" e a "Normal da Face". Se o ângulo for pequeno, a face fica clara. Se a luz estiver batendo "atrás" da normal, a face fica escura.
    
- **Colisão:** Quando uma bola bate numa parede, ela ricocheteia com base na Normal da parede. Sem a normal, a bola não saberia para onde voltar.
    
- **Backface Culling:** O computador usa a normal para saber se o triângulo está virado para a câmera. Se a normal estiver apontando para o lado oposto, o computador nem desenha aquele triângulo (para economizar processamento).
    

---

## 4. Normal vs. Normalizado (Cuidado!)

Não confunda os nomes:

- **Vetor Normal:** É o vetor perpendicular à superfície (pode ter qualquer tamanho).
    
- **Vetor Normalizado:** É qualquer vetor que foi "encolhido" ou "esticado" para ter **módulo igual a 1** (unitário).
    

> **Dica de Ouro:** Quase sempre, na Computação Gráfica, depois de encontrar a **Normal** (via produto vetorial), nós a **Normalizamos** (dividimos pelo módulo) para que os cálculos de luz funcionem corretamente.

Ficou claro que ser "Normal" é apenas estar "em pé" em relação a uma superfície?

Como você já está craque no produto vetorial, quer que eu te mostre como calcular a **Normal Unitária** (o passo final para a iluminação) usando os pontos $p_0, p_1$ e $p_2$?