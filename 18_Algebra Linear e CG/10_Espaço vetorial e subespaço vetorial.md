
#Concluded 

---
### **1. Espaço vetorial**

Um **Espaço Vetorial** é um conjunto não vazio $V$, cujos elementos chamamos de **vetores**, sobre o qual definimos duas operações:
1. **Soma de vetores:** Você pega dois vetores e gera um terceiro no mesmo conjunto ($u + v$).
2. **Multiplicação por escalar:** Você pega um número real e multiplica por um vetor ($\alpha \cdot u$).

Para ser considerado um Espaço Vetorial, essas operações precisam respeitar **8 axiomas fundamentais.

Sejam $u, v, w \in V$ vetores e $\alpha, \beta \in \mathbb{R}$ escalares:

1. **Comutativa:** A ordem não altera o resultado.$$u + v = v + u$$
2. **Associativa:** O agrupamento não altera o resultado.$$(u + v) + w = u + (v + w)$$
3. **Elemento Neutro:** Existe um vetor "zero" que não altera ninguém.$$\exists \mathbf{0} \in V \mid u + \mathbf{0} = u$$
4. **Elemento Oposto:** Todo vetor tem um "espelho" que o anula.$$\forall u \in V, \exists (-u) \in V \mid u + (-u) = \mathbf{0}$$
5. **Distributiva (em relação à soma de vetores):**$$\alpha(u + v) = \alpha u + \alpha v$$
6. **Distributiva (em relação à soma de escalares):**$$(\alpha + \beta)u = \alpha u + \beta u$$
7. **Associativa da Multiplicação:**$$\alpha(\beta u) = (\alpha \beta)u$$
8. **Elemento Neutro da Multiplicação:** O número 1 mantém o vetor original.$$1 \cdot u = u$$
---
### 2. Subespaço vetorial

Seja $V$ um espaço vetorial. Um subconjunto $W \subseteq V$ é um **subespaço vetorial** de $V$ se, e somente se, as seguintes condições forem satisfeitas:

1. **O Vetor Nulo está presente:** $$\mathbf{0} \in W$$
2. **Fechamento na Soma:** $$\forall u, v \in W \implies (u + v) \in W$$
3. **Fechamento na Multiplicação por Escalar:** $$\forall u \in W, \forall \alpha \in \mathbb{R} \implies (\alpha u) \in W$$

>[!note]
>Sejam $W_{1}$ e $W_{2}$ subespaços do espaço vetorial $V$. Então a interseção  $W_{1} \cap W_{2}$  é um subespaço  de $V$.

>[!note]
Se $U$ e $W$ são subespaços de um espaço vetorial $V$, a soma é definida como:
$$U + W = \{ u + w \mid u \in U, w \in W \}$$
Ou seja, você pega todos os elementos de $U$, soma com todos os elementos de $W$, e o "pacotão" de resultados forma o novo subespaço.
