

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

---
#### **2. Normalização da Projeção Oblíqua**

A projeção oblíqua é uma projeção paralela que simula profundidade através de raios de projeção inclinados. A normalização dessa projeção é obtida aplicando um Cisalhamento para desfazer a inclinação desses raios inclinados, seguido pela Normalização Ortográfica.
$$M_{obl}=M_{ortho}\cdot T_{post}\cdot M_{shear}\cdot T_{pre}$$

O cisalhamento é aplicado em uma sequência de 3 etapas para preservar as dimensões do volume ortográfico original, apenas desfazendo a inclinação dos raios de projeção:

- Pré-Translação ($T_{pre}$): Move o plano frontal $Z_{cam}=-n$ para $Z_{cam}=0$.
- Cisalhamento ($M_{shear}$): Desfaz a inclinação.
- Pós-Translação ($T_{post}$): Devolve o plano frontal para $Z_{cam}=-n$.

Na projeção oblíqua, o cisalhamento é aplicado em X e Y mantendo Z fixo:
$$M_{shear}=\begin{bmatrix}1&0&sh_{x}&0\\ 0&1&sh_{y}&0\\ 0&0&1&0\\ 0&0&0&1\end{bmatrix}$$

Para garantir que a face frontal do volume não se desloque durante o cisalhamento, aplicamos uma sequência de Translação Prévia, Cisalhamento e Translação Posterior, resultando na matriz de cisalhamento total ($M_{shear}^{\prime}$).

Os fatores de cisalhamento ($sh_{x},sh_{y}$) são calculados a partir do ângulo de inclinação do raio de projeção ($\alpha$) e do fator de escala de profundidade ($s$, onde $s\in[0,1]$): $sh_{x}=sh_{y}=s\cdot cot(\alpha)$.

$$T_{pre}=\begin{bmatrix}1&0&0&0\\ 0&1&0&0\\ 0&0&1&n\\ 0&0&0&1\end{bmatrix}$$

$$M_{shear}=\begin{bmatrix}1&0&sh_{x}&0\\ 0&1&sh_{y}&0\\ 0&0&1&0\\ 0&0&0&1\end{bmatrix}$$

$$T_{post}=\begin{bmatrix}1&0&0&0\\ 0&1&0&0\\ 0&0&1&-n\\ 0&0&0&1\end{bmatrix}$$

O produto das transformações resulta na matriz de cisalhamento total ($M_{shear}^{\prime}$):
$$M_{shear}^{\prime}=\begin{bmatrix}1&0&sh_{x}&n\cdot sh_{x}\\ 0&1&sh_{y}&n\cdot sh_{y}\\ 0&0&1&0\\ 0&0&0&1\end{bmatrix}$$

A matriz final é $M_{obl}=M_{ortho}\cdot M_{shear}^{\prime}$.

$$M_{obl}=\begin{bmatrix}\frac{2}{r-l}&0&0&-\frac{l+r}{r-l}\\ 0&\frac{2}{t-b}&0&-\frac{t+b}{t-b}\\ 0&0&\frac{2}{f-n}&\frac{f+n}{f-n}\\ 0&0&0&1\end{bmatrix}\cdot\begin{bmatrix}1&0&sh_{x}&n\cdot sh_{x}\\ 0&1&sh_{y}&n\cdot sh_{y}\\ 0&0&1&0\\ 0&0&0&1\end{bmatrix}$$


A projeção oblíqua é um tipo de projeção paralela que tem como principal propósito preservar a ortogonalidade (ângulos de 90 graus) e as dimensões reais de uma face do objeto em relação ao plano de projeção, enquanto ainda oferece uma percepção de profundidade tridimensional.

Existem dois tipos principais, definidos pelo fator de escala da profundidade:
- s=1: A profundidade não é reduzida; tende a parecer alongada
- s=0.5: A profundidade é reduzida à metade, oferecendo um visual mais realista.


---
#### **3. Normalização perspectiva**

A projeção perspectiva transforma o frustum de visualização (tronco de pirâmide) no Cubo Canônico de Visualização (CCV). A matriz final de normalização é uma composição de três etapas:
$$M_{frustum}=M_{persp}\cdot S_{ang}\cdot M_{shear}$$

- $M_{shear}$ Cisalhamento para tornar o frustum simétrico (centro em $X=0,Y=0$).
    ![300](../attachments/Pasted%20image%2020260602083540.png)
- $S_{ang}:$ Escala para normalizar os ângulos de abertura, ajustando o tamanho da face frontal para a dimensão padrão de $2n\times2n$.
    ![300](../attachments/Pasted%20image%2020260602083608.png)
- $M_{persp}$: Matriz que aplica a lógica da perspectiva (Divisão por Z) e o mapeamento de Z ($\alpha~e~\beta$).

#### **3.1 Cisalhamento ($M_{shear}$)**
O objetivo do cisalhamento é deslocar o centro do retângulo do plano near para (0,0). 

- **Fator de Cisalhamento**:  $sh_{x}=\frac{l+r}{2n}$
- **Fator de Cisalhamento**:  $sh_{y}=\frac{b+t}{2n}$.
$$M_{shear}=\begin{pmatrix}1&0&\frac{l+r}{2n{}}&0\\ 0&1&\frac{b+t}{2n}&0\\ 0&0&1&0\\ 0&0&0&1\end{pmatrix}$$

#### **3.2 Escala**
A escala $S_{ang}$ é aplicada para que as novas dimensões do frustum no plano near sejam $2n\times2n$. 
- **Fator de Escala $S_{x}$**: A largura atual ($r-l$) deve ser ajustada para 2n. Logo, $S_{x}=\frac{2n}{r-l}.$
- **Fator de Escala $S_{y}$**: A altura atual ($t-b$) deve ser ajustada para 2n. Logo, $S_{y}=\frac{2n}{t-b}$

$$S_{ang}=\begin{pmatrix}\frac{2n}{r-1}&0&0&0\\ 0&\frac{2n}{t-b}&0&0\\ 0&0&1&0\\ 0&0&0&1\end{pmatrix}$$
### 3.3 


#### **3.4 Matriz final**
$$M_{fratum}=\begin{pmatrix}\frac{2n}{r-l}&0&\frac{l+r}{r-l}&0\\ 0&\frac{2n}{t-b}&\frac{b+t}{t-b}&0\\ 0&0&\frac{f+n}{f-n}&\frac{2fn}{f-n}\\ 0&0&-1&0\end{pmatrix}$$
