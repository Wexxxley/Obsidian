
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

**Mudança de vetor da conônica para nova base**
![](../attachments/20260312_194344648.jpg)

**Mudança de base para a canônica**
![](../attachments/20260312_194409843.jpg)

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

### **3. Base ortonormal

Para que um conjunto de vetores (como uma base de um espaço vetorial) seja considerado ortonormal, ele deve satisfazer simultaneamente duas condições: a **ortogonalidade** e a **normalidade**.

**Ortogonalidade**: Dizemos que dois vetores são ortogonais quando o produto escalar entre eles é igual a zero. Isso significa que eles são perpendiculares entre si, formando um ângulo de 90°.

**Normalidade**: Um vetor é considerado "normal"quando o seu comprimento é exatamente igual a 1. 
- Para um vetor $\vec{u}$ ser normal, o produto escalar dele por ele mesmo deve ser 1, pois:
$$\vec{u} \cdot \vec{u} = \|\vec{u}\|^2 = 1^2 = 1$$

