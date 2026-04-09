
---

As transformações lineares em 3D são funções matemáticas que mapeiam um vetor de entrada $(x, y, z)$ para um novo vetor de saída $(x', y', z')$.

Toda transformação linear pode ser representada por uma **Matriz de Transformação**. Em 3D, usamos matrizes $3 \times 3$ (ou $4 \times 4$ para coordenadas homogêneas).

### **1. Translatar**

Transladar um ponto significa somar um deslocamento: $x' = x + t_x$. As outras transformações (escala, rotação, cisalhamento) são multiplicações. Se você mantiver o 3D puro, não consegue combinar o movimento com o giro em uma única matriz. Você teria que multiplicar para girar e depois somar para mover, o que impede a otimização em massa que as GPUs fazem.

Para transformar a soma em uma multiplicação, "fingimos" que o nosso mundo 3D existe dentro de um espaço 4D. 



Vamos usar a segunda matriz da sua imagem (a correta, $4 \times 4$). Imagine que você quer mover um ponto do seu objeto em Quixadá por **10 unidades em X** e **5 unidades em Z**.

**Configuração:**

- $t_x = 10, t_y = 0, t_z = 5$
    
- Ponto original $P = (1, 1, 1)$ → Em coordenadas homogêneas: $\begin{pmatrix} 1 \\ 1 \\ 1 \\ 1 \end{pmatrix}$
    

**A conta matricial:**

$$\begin{bmatrix} 1 & 0 & 0 & \mathbf{10} \\ 0 & 1 & 0 & \mathbf{0} \\ 0 & 0 & 1 & \mathbf{5} \\ 0 & 0 & 0 & 1 \end{bmatrix} \cdot \begin{bmatrix} 1 \\ 1 \\ 1 \\ 1 \end{bmatrix}$$

**Resultado linha por linha:**

- $x' = (1 \cdot 1) + (0 \cdot 1) + (0 \cdot 1) + (10 \cdot 1) = \mathbf{11}$
    
- $y' = (0 \cdot 1) + (1 \cdot 1) + (0 \cdot 1) + (0 \cdot 1) = \mathbf{1}$
    
- $z' = (0 \cdot 1) + (0 \cdot 1) + (1 \cdot 1) + (5 \cdot 1) = \mathbf{6}$
    
- $w' = (0 \cdot 1) + (0 \cdot 1) + (0 \cdot 1) + (1 \cdot 1) = \mathbf{1}$
    

---

### 4. A Grande Vantagem: Concatenação

Agora que a translação é uma matriz $4 \times 4$, você pode fazer isso aqui no seu código:

$$M_{final} = M_{translacao} \cdot M_{rotacao} \cdot M_{escala}$$

O resultado é uma única matriz $4 \times 4$ que, ao ser multiplicada por um ponto, **muda o tamanho, gira e move o objeto para o lugar certo de uma vez só**. Sem essa quarta dimensão, você teria que aplicar cada operação em passos separados, o que tornaria jogos modernos impossíveis de rodar.

Ficou claro como o $1$ do final do vetor "ativa" os valores de $t_x, t_y, t_z$ durante a multiplicação?
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


- **Rotação no eixo Z:** $$R_z(\theta) = \begin{bmatrix} \cos\theta & -\sin\theta & 0 \\ \sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{bmatrix}$$![500](../attachments/20260409_155417254.jpg)
 
### **3. Reflexão**

A reflexão inverte o objeto em relação a um plano (como um espelho).

- **Matriz de Reflexão no plano XY:** Basta inverter o sinal do componente Z.
    
    $$Ref_{xy} = \begin{bmatrix} 1 & 0 & 0 \\ 0 & 1 & 0 \\ 0 & 0 & -1 \end{bmatrix}$$

![500](../attachments/Pasted%20image%2020260314173140.png)

![400](../attachments/Pasted%20image%2020260314173748.png)
![400](../attachments/Pasted%20image%2020260314173809.png)
