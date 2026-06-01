

---

Basicamente eu deformo/mapeio o que está dentro do volume de visualização para dentro do cubo canônico.
![250](../attachments/Pasted%20image%2020260601074327.png)
**Cubo canônico**
![200](../attachments/Pasted%20image%2020260601070659.png)

### **1. Normalização projeção ortográfica**

Para delimitar as fronteiras exatas do volume de visualização, estabelecemos seis planos de recorte;
- **Eixo X:** Definido pelo plano esquerdo $l$, e pelo plano direito $r$.
- **Eixo Y:** Definido pelo plano inferior $b$, e pelo plano superior $t$.
- **Eixo Z** Definido pelo plano próximo $n$, e pelo plano distante $f$. Aqui utilizamos as distâncias

Primeiramente, é necessário deslocar o centro do volume ortográfico para que este coincida com a origem geométrica $(0,0,0)$. Portanto, o centro do volume é dado:
$$centro = \left(\frac{r+l}{2}, \frac{t+b}{2}, \frac{n+f}{2}\right)$$

A matriz de translação $T$ subtrai estes valores das coordenadas de qualquer vértice:
$$T = \begin{bmatrix} 1 & 0 & 0 & -\frac{r+l}{2} \\ 0 & 1 & 0 & -\frac{t+b}{2} \\ 0 & 0 & 1 & -\frac{n+f}{2} \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

Para ajustar as dimensões, aplica-se uma matriz de escala $S$ cujos fatores são a razão entre a dimensão desejada ($2$) e a dimensão atual em cada eixo:

$$S = \begin{bmatrix} \frac{2}{r-l} & 0 & 0 & 0 \\ 0 & \frac{2}{t-b} & 0 & 0 \\ 0 & 0 & \frac{2}{n-f} & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

A matriz final de projeção ortográfica $M_{\text{orto}}$ é obtida através da multiplicação matricial $S \times T$. 
$$M_{\text{orto}} = \begin{bmatrix} \frac{2}{r-l} & 0 & 0 & -\frac{r+l}{r-l} \\ 0 & \frac{2}{t-b} & 0 & -\frac{t+b}{t-b} \\ 0 & 0 & \frac{2}{n-f} & -\frac{n+f}{n-f} \\ 0 & 0 & 0 & 1 \end{bmatrix}$$
