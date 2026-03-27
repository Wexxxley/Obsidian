
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

- Se temos dois vetores distintos $\vec{u}$ e $\vec{v}$ de um conjunto, a condição de ortogonalidade exige que:
    
    $$\vec{u} \cdot \vec{v} = 0$$
    
- Em termos práticos, se você projetar um vetor sobre o outro, a projeção será nula, indicando que um vetor não possui "componente" na direção do outro.
    

## **2. Normalidade (Vetores Unitários)**

Um vetor é considerado "normal" ou "normalizado" quando o seu comprimento (módulo ou norma) é exatamente igual a 1. Esses são os chamados **vetores unitários**.

- Para um vetor $\vec{u}$ ser normal, o produto escalar dele por ele mesmo deve ser 1, pois:
    
    $$\vec{u} \cdot \vec{u} = \|\vec{u}\|^2 = 1^2 = 1$$
    
- Se um vetor não for unitário, podemos normalizá-lo dividindo cada um de seus componentes pelo seu módulo total.
    

## **3. Definição Sintetizada**

Portanto, um conjunto de vetores $\{v_1, v_2, ..., v_n\}$ é **ortonormal** se, para quaisquer índices $i$ e $j$, o produto escalar seguir a regra do Delta de Kronecker ($\delta_{ij}$):

- **Se $i \neq j$:** O produto escalar é **0** (são ortogonais).
    
- **Se $i = j$:** O produto escalar é **1** (são unitários).
    

## **4. Importância na Computação**

Como você estuda Ciência da Computação, a ortonormalidade é fundamental por dois motivos principais:

- **Simplificação de Cálculos:** Em bases ortonormais, encontrar as coordenadas de um ponto é muito mais simples (basta usar produtos escalares diretos, sem resolver grandes sistemas lineares).
    
- **Matrizes Ortogonais:** Como vimos no exercício anterior, as matrizes cujas colunas são vetores ortonormais possuem a propriedade de que sua **inversa é igual à sua transposta** ($M^{-1} = M^T$). Isso é o padrão ouro em transformações de rotação em computação gráfica, pois economiza processamento.
    

---

Gostaria que eu demonstrasse como verificar se um conjunto específico de vetores é ortonormal através de um exemplo numérico?