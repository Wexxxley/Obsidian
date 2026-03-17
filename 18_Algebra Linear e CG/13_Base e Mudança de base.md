
#Concluded 

---
### **1. Base**

Para um conjunto de vetores ser considerado uma base de um espaço $V$, ele precisa obrigatoriamente cumprir duas condições:

1. Tem que serem **linearmente independentes.**
2. Combinando esses vetores, você deve ser capaz de alcançar qualquer ponto dentro do espaço vetorial $V$.

![500](../attachments/20260312_191853029.jpg)

---
### 2. Mudança de base

A mudança de base é o processo de converter as coordenadas de um vetor de um sistema de referência para outro.

- A **Base Canônica** no $\mathbb{R}^2$ é formada por $(1, 0) ,(0, 1)$.
- Mas você pode inventar outra base $\beta = \{v_1, v_2\}$ qualquer.
#### **1. Maneira simples**

**Mudança de vetor da conônica para nova base**
![](../attachments/20260312_194344648.jpg)

**Mudança de base para a canônica**
![](../attachments/20260312_194409843.jpg)

#### **2. Matriz de mudança de base**

Considere duas bases no $\mathbb{R}^2$:
- **Base Canônica ($\epsilon$):** $e_1 = (1, 0), e_2 = (0, 1)$
- **Base Qualquer ($\beta$):** $v_1 = (1, 2), v_2 = (3, 4)$
    

**De uma Base $\beta$ para a Canônica $\epsilon$**
Monte a matriz $M$ colocando os vetores de $\beta$ nas **colunas**.
$$M = \begin{bmatrix} v_{1x} & v_{2x} \\ v_{1y} & v_{2y} \end{bmatrix}$$

$$[v]_\epsilon = M \cdot [v]_\beta$$

**Da Canônica $\epsilon$ para uma Base $\beta$**

$$[v]_\beta = M^{-1} \cdot [v]_\epsilon$$


---

## 2. Aplicação com Valores Reais

### Problema A: Converter de $\beta$ para a Canônica

Seja o vetor $[v]_\beta = \begin{bmatrix} 5 \\ -2 \end{bmatrix}$ (ou seja, ele é feito de $5 \cdot v_1 - 2 \cdot v_2$). Qual o valor dele em $(x, y)$ normal?

**Cálculo:**

$$[v]_\epsilon = \begin{bmatrix} 1 & 3 \\ 2 & 4 \end{bmatrix} \begin{bmatrix} 5 \\ -2 \end{bmatrix} = \begin{bmatrix} 1(5) + 3(-2) \\ 2(5) + 4(-2) \end{bmatrix} = \begin{bmatrix} 5 - 6 \\ 10 - 8 \end{bmatrix} = \mathbf{\begin{bmatrix} -1 \\ 2 \end{bmatrix}}$$

---

### Problema B: Converter da Canônica para $\beta$

Seja o vetor $[v]_\epsilon = \begin{bmatrix} 7 \\ 10 \end{bmatrix}$. Quais as coordenadas dele na base $\beta$?

**1. Primeiro, ache a inversa de $M$:**

$\text{det}(M) = (1 \cdot 4) - (3 \cdot 2) = -2$

$$M^{-1} = \frac{1}{-2} \begin{bmatrix} 4 & -3 \\ -2 & 1 \end{bmatrix} = \begin{bmatrix} -2 & 1.5 \\ 1 & -0.5 \end{bmatrix}$$

**2. Aplique a fórmula:**

$$[v]_\beta = \begin{bmatrix} -2 & 1.5 \\ 1 & -0.5 \end{bmatrix} \begin{bmatrix} 7 \\ 10 \end{bmatrix} = \begin{bmatrix} -2(7) + 1.5(10) \\ 1(7) - 0.5(10) \end{bmatrix} = \begin{bmatrix} -14 + 15 \\ 7 - 5 \end{bmatrix} = \mathbf{\begin{bmatrix} 1 \\ 2 \end{bmatrix}}$$

---

## 3. Resumo de Uso (Checklist)

- **Vetor na base nova $\to$ Vetor "normal" $(x,y)$:** Multiplique pela matriz das colunas.
    
- **Vetor "normal" $(x,y) \to$ Vetor na base nova:** Multiplique pela inversa da matriz.
    
- **Entre duas bases doidas ($\beta \to \gamma$):** $[v]_\gamma = (M_\gamma)^{-1} \cdot M_\beta \cdot [v]_\beta$.
    

Precisa que eu resolva algum exercício específico da sua lista da UFC usando esse passo a passo?