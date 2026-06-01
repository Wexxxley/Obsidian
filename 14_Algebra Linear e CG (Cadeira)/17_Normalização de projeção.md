

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

#### **2. Normalização da Projeção Oblíqua**
Aqui está a extração literal das explicações referentes à projeção oblíqua presentes no documento fornecido:

3 Projeção Oblíqua

A projeção oblíqua é uma projeção paralela que simula profundidade através de raios de projeção inclinados. A normalização dessa projeção é obtida aplicando um Cisalhamento ($M_{shear}$) para desfazer a inclinação desses raios inclinados (e do volume de visualização inclinado correspondente), seguido pela Normalização Ortográfica ($M_{ortho}$).

$$M_{obl}=M_{ortho}\cdot T_{post}\cdot M_{shear}\cdot T_{pre}$$

O cisalhamento é aplicado em uma sequência de 3 etapas para preservar as dimensões do volume ortográfico original, apenas desfazendo a inclinação dos raios de projeção:

- 1. Pré-Translação ($T_{pre}$): Move o plano frontal $Z_{cam}=-n$ para $Z_{cam}=0$.
    
- 2. Cisalhamento ($M_{shear}$): Desfaz a inclinação.
    
- 3. Pós-Translação ($T_{post}$): Devolve o plano frontal para $Z_{cam}=-n$.
    

3.1 Cisalhamento (Shear)

O cisalhamento é uma transformação que move cada ponto em uma direção específica (exemplo, X) por uma quantidade proporcional à sua distância de um eixo ou plano.

**Cisalhamento 3D para Projeção Oblíqua** Na projeção oblíqua, o cisalhamento é aplicado em X e Y em função de Z, mantendo Z fixo:

$$\begin{cases}x^{\prime}=x+sh_{x}\cdot z\\ y^{\prime}=y+sh_{y}\cdot z\\ z^{\prime}=z\end{cases}$$

onde $sh_{x}=sh_{y}=s\cdot cot(\alpha)$

$$M_{shear}=\begin{bmatrix}1&0&sh_{x}&0\\ 0&1&sh_{y}&0\\ 0&0&1&0\\ 0&0&0&1\end{bmatrix}$$

Para garantir que a face frontal do volume ($Z_{cam}=-n$) não se desloque durante o cisalhamento, aplicamos uma sequência de Translação Prévia ($T_{pre}$), Cisalhamento ($M_{shear}$) e Translação Posterior ($T_{post}$), resultando na matriz de cisalhamento total ($M_{shear}^{\prime}$).

3.2 Cisalhamento e Translações

Os fatores de cisalhamento ($sh_{x},sh_{y}$) são calculados a partir do ângulo de inclinação do raio de projeção ($\alpha$) e do fator de escala de profundidade ($s$, onde $s\in[0,1]$): $sh_{x}=sh_{y}=s\cdot cot(\alpha)$.

- **Pré-Translação ($T_{pre}$):** Desloca Z de -n para 0.
    
- **Cisalhamento ($M_{shear}$):**
    
- **Pós-Translação ($T_{post}$):** Desloca Z de 0 para -n.
    

$$T_{pre}=\begin{bmatrix}1&0&0&0\\ 0&1&0&0\\ 0&0&1&n\\ 0&0&0&1\end{bmatrix}$$

$$M_{shear}=\begin{bmatrix}1&0&sh_{x}&0\\ 0&1&sh_{y}&0\\ 0&0&1&0\\ 0&0&0&1\end{bmatrix}$$

$$T_{post}=\begin{bmatrix}1&0&0&0\\ 0&1&0&0\\ 0&0&1&-n\\ 0&0&0&1\end{bmatrix}$$

O produto das transformações $T_{post}\cdot M_{shear}\cdot T_{pre}$ resulta na matriz de cisalhamento total ($M_{shear}^{\prime}$):

$$M_{shear}^{\prime}=\begin{bmatrix}1&0&sh_{x}&n\cdot sh_{x}\\ 0&1&sh_{y}&n\cdot sh_{y}\\ 0&0&1&0\\ 0&0&0&1\end{bmatrix}$$

3.3 Matriz Final ($M_{obl}$)

A matriz final é $M_{obl}=M_{ortho}\cdot M_{shear}^{\prime}$.

$$M_{obl}=\begin{bmatrix}\frac{2}{r-l}&0&0&-\frac{l+r}{r-l}\\ 0&\frac{2}{t-b}&0&-\frac{t+b}{t-b}\\ 0&0&\frac{2}{f-n}&\frac{f+n}{f-n}\\ 0&0&0&1\end{bmatrix}\cdot\begin{bmatrix}1&0&sh_{x}&n\cdot sh_{x}\\ 0&1&sh_{y}&n\cdot sh_{y}\\ 0&0&1&0\\ 0&0&0&1\end{bmatrix}$$

3.4 Propósito e Uso

A projeção oblíqua é um tipo de projeção paralela que tem como principal propósito preservar a ortogonalidade (ângulos de 90 graus) e as dimensões reais de uma face do objeto em relação ao plano de projeção, enquanto ainda oferece uma percepção de profundidade tridimensional.

**Para que Serve?**

A projeção oblíqua é amplamente utilizada em desenho técnico, arquitetura e engenharia para criar representações que são:

- **Fácil de Medir:** Uma das faces do objeto (geralmente a frontal) é desenhada em escala verdadeira (sem distorção), tornando as dimensões diretas e fáceis de ler.
    
- **Melhor Visualização de Profundidade do que a Ortográfica:** Ao contrário da projeção ortográfica pura, onde a profundidade é plana, a oblíqua inclina o eixo de profundidade, proporcionando uma noção de volume.
    
- **Menos Distorção de Linhas Paralelas do que a Perspectiva:** Como é uma projeção paralela, linhas que são paralelas na cena permanecem paralelas na imagem projetada (ao contrário da perspectiva, onde elas convergem para os pontos de fuga).
    

Existem dois tipos principais, definidos pelo fator de escala da profundidade:

| **Tipo**     | **Fator de Profundidade (s)** | **Características**                                                     |
| ------------ | ----------------------------- | ----------------------------------------------------------------------- |
| **Cavalier** | $s=1$                         | A profundidade não é reduzida; tende a parecer alongada.                |
| **Cabinet**  | $s=0.5$                       | A profundidade é reduzida à metade, oferecendo um visual mais realista. |