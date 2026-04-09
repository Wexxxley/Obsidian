
---

As transformações lineares em 3D são funções matemáticas que mapeiam um vetor de entrada $(x, y, z)$ para um novo vetor de saída $(x', y', z')$.

Toda transformação linear pode ser representada por uma **Matriz de Transformação**. Em 3D, usamos matrizes $3 \times 3$ (ou $4 \times 4$ para coordenadas homogêneas).

### **1. Escala**

A escala altera o tamanho do objeto. Ela multiplica cada componente do vetor por um fator de escala $s$.
 $$S = \begin{bmatrix} s_x & 0 & 0 \\ 0 & s_y & 0 \\ 0 & 0 & s_z \end{bmatrix}$$    
- Se $s_x = 2$, o objeto dobra de largura. Se for $0.5$, ele reduz pela metade. Se os fatores forem diferentes, você "estica" o objeto em direções específicas.
	![500](../attachments/20260409_154512420.jpg)

---
### **2. Rotação**

A rotação em 3D é mais complexa que em 2D porque você precisa definir um **eixo de rotação**. As matrizes mudam dependendo de qual eixo o objeto gira:

- **Rotação no Eixo X**
$$R_x(\theta) = \begin{bmatrix} 1 & 0 & 0 \\ 0 & \cos\theta & -\sin\theta \\ 0 & \sin\theta & \cos\theta \end{bmatrix}$$

- **Rotação no eixo Y**
$$R_y(\theta) = \begin{bmatrix} \cos\theta & 0 & \sin\theta \\ 0 & 1 & 0 \\ -\sin\theta & 0 & \cos\theta \end{bmatrix}$$


- **Rotação no eixo Z:** $$R_z(\theta) = \begin{bmatrix} \cos\theta & -\sin\theta & 0 \\ \sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{bmatrix}$$
 
### 3. Cisalhamento (Shear)

O cisalhamento "inclina" o objeto. Ele faz com que uma coordenada mude proporcionalmente ao valor de outra coordenada.

- **Exemplo:** Inclinar o objeto no eixo X com base na sua altura (Z).
    
- **Visualização:** Imagine um cubo de gelatina sendo empurrado no topo enquanto a base continua fixa. As faces que eram quadradas tornam-se paralelogramos.
    

---

### 4. Reflexão (Reflection)

A reflexão inverte o objeto em relação a um plano (como um espelho).

- **Matriz de Reflexão no plano XY:** Basta inverter o sinal do componente Z.
    
    $$Ref_{xy} = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & -1 \end{bmatrix}$$
    

---

### 5. O papel das Matrizes e o Vetor Coluna

Como discutimos antes, para aplicar essas transformações, você coloca a matriz à esquerda e o seu vetor (ponto do objeto) como uma **coluna** à direita:

$$\begin{bmatrix} x' \\ y' \\ z' \end{bmatrix} = \begin{bmatrix} \text{Matriz de} \\ \text{Transformação} \end{bmatrix} \cdot \begin{bmatrix} x \\ y \\ z \end{bmatrix}$$

### Por que a Translação não está aqui?

Tecnicamente, a **Translação** (mover o objeto de lugar) **não é uma transformação linear** em 3D puro, porque ela não leva a origem na origem (você soma um valor, não multiplica).

Para resolver isso na computação gráfica, usamos **Coordenadas Homogêneas** (matrizes $4 \times 4$). Com elas, transformamos a translação em uma operação linear em um espaço de 4 dimensões, permitindo que multipliquemos matrizes para girar e mover ao mesmo tempo.

Ficou claro como essas matrizes "moldam" os vetores no espaço? Gostaria de ver um exemplo numérico de como girar um ponto específico, como o $(1, 0, 0)$, em 90 graus no eixo Z?


![500](../attachments/Pasted%20image%2020260314173140.png)

![400](../attachments/Pasted%20image%2020260314173748.png)
![400](../attachments/Pasted%20image%2020260314173809.png)
