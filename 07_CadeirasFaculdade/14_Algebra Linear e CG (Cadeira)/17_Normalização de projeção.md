

---
Basicamente eu deformo/mapeio o que está dentro do volume de visualização para dentro do cubo canônico.
![250](../../attachments/Pasted%20image%2020260601074327.png)
**Cubo canônico**
![200](../../attachments/Pasted%20image%2020260601070659.png)

### **1. Normalização projeção ortográfica**

- **Eixo X:** Definido pelo plano esquerdo $l$, e pelo plano direito $r$.
- **Eixo Y:** Definido pelo plano inferior $b$, e pelo plano superior $t$.
- **Eixo Z** Definido pelo plano próximo $n$, e pelo plano distante $f$. Aqui utilizamos as distâncias

Primeiramente, é deslocado o centro do volume para que coincida com a origem $(0,0,0)$. 
$$centro Do Volume Ortográfico = \left(\frac{r+l}{2}, \frac{t+b}{2}, \frac{f+n}{2}\right)$$
A matriz de translação $T$ subtrai estes valores das coordenadas de qualquer vértice:
$$T = \begin{bmatrix} 1 & 0 & 0 & -\frac{r+l}{2} \\ 0 & 1 & 0 & -\frac{t+b}{2} \\ 0 & 0 & 1 & \frac{f+n}{2} \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

Para ajustar as dimensões, aplica-se uma matriz de escala $S$ cujos fatores são a razão entre a dimensão desejada ($2$) e a dimensão atual em cada eixo:

$$S = \begin{bmatrix} \frac{2}{r-l} & 0 & 0 & 0 \\ 0 & \frac{2}{t-b} & 0 & 0 \\ 0 & 0 & -\frac{2}{f-n} & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

A matriz de projeção ortográfica $M_{\text{orto}}$ é obtida através da multiplicação matricial $S \times T$. 
$$M_{\text{orto}} = \begin{bmatrix} \frac{2}{r-l} & 0 & 0 & -\frac{r+l}{r-l} \\ 0 & \frac{2}{t-b} & 0 & -\frac{t+b}{t-b} \\ 0 & 0 & -\frac{2}{f-n} & -\frac{f+n}{f-n} \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

_glOrtho(left, right, bottom, top, near, far)_.

---
#### **2. Normalização da Projeção Oblíqua**

$$M_{obl}=M_{ortho}\cdot T_{post}\cdot M_{shear}\cdot T_{pre}$$

O cisalhamento é aplicado em uma sequência de 3 etapas para preservar as dimensões do volume ortográfico original, apenas desfazendo a inclinação dos raios de projeção:

- Pré-Translação ($T_{pre}$): Move o plano frontal para 0
- Cisalhamento ($M_{shear}$): Desfaz a inclinação. Aplicado em X e Y mantendo Z fixo:
- Pós-Translação ($T_{post}$): Devolve o plano frontal para a posição original

Os fatores de cisalhamento ($sh_{x},sh_{y}$) são calculados a partir do ângulo de inclinação do raio de projeção ($\alpha$) e do fator de escala de profundidade ($s$, onde $s\in[0,1]$): $sh_{x}=sh_{y}=s\cdot cot(\alpha)$.
$$T_{pre}=\begin{bmatrix}1&0&0&0\\ 0&1&0&0\\ 0&0&1&n\\ 0&0&0&1\end{bmatrix}$$

$$M_{shear}=\begin{bmatrix}1&0&sh_{x}&0\\ 0&1&sh_{y}&0\\ 0&0&1&0\\ 0&0&0&1\end{bmatrix}$$

$$T_{post}=\begin{bmatrix}1&0&0&0\\ 0&1&0&0\\ 0&0&1&-n\\ 0&0&0&1\end{bmatrix}$$

O produto das transformações resulta na matriz de cisalhamento total ($M_{shear}^{\prime}$):
$$M_{shear}^{\prime}=\begin{bmatrix}1&0&sh_{x}&n\cdot sh_{x}\\ 0&1&sh_{y}&n\cdot sh_{y}\\ 0&0&1&0\\ 0&0&0&1\end{bmatrix}$$

A matriz final é $M_{obl}=M_{ortho}\cdot M_{shear}^{\prime}$.

$$M_{obl}=\begin{bmatrix}\frac{2}{r-l}&0&0&-\frac{l+r}{r-l}\\ 0&\frac{2}{t-b}&0&-\frac{t+b}{t-b}\\ 0&0&\frac{2}{f-n}&\frac{f+n}{f-n}\\ 0&0&0&1\end{bmatrix}\cdot\begin{bmatrix}1&0&sh_{x}&n\cdot sh_{x}\\ 0&1&sh_{y}&n\cdot sh_{y}\\ 0&0&1&0\\ 0&0&0&1\end{bmatrix}$$

Existem dois tipos principais, definidos pelo fator de escala da profundidade:
- s=1: A profundidade não é reduzida; tende a parecer alongada
- s=0.5: A profundidade é reduzida à metade, oferecendo um visual mais realista.

---
#### **3. Normalização perspectiva**

A projeção perspectiva transforma o frustum de visualização (tronco de pirâmide) no Cubo Canônico de Visualização (CCV). A matriz final de normalização é uma composição de três etapas:
$$M_{frustum}=M_{persp}\cdot S_{ang}\cdot M_{shear}$$

- $M_{shear}$ Cisalhamento para tornar o frustum simétrico (centro em $X=0,Y=0$).
    ![300](../../attachments/Pasted%20image%2020260602083540.png)
- $S_{ang}:$ Escala para normalizar os ângulos de abertura, ajustando o tamanho da face frontal para a dimensão padrão de $2n\times2n$.
    ![300](../../attachments/Pasted%20image%2020260602083608.png)
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
### 3.3 Matriz de perspectiva

A matriz $M_{persp}$ finaliza a transformação do frustum simétrico normalizado para o CCV.

O Teorema de Tales é o princípio geométrico fundamental que governa a projeção perspectiva. O cenário da projeção perspectiva envolve três elementos, que formam um triângulo retângulo na vista superior:

- Câmera: Localizado na origem (0,0,0).
    
- Plano de Projeção (Imagem): Localizado em uma distância d do observador. No nosso sistema de câmera (onde o observador olha para -Z), o plano está em $Z_{proj}=d$ (onde d é negativo, e.g., $d=-1$).
    
- Ponto na Cena P: Um ponto que está sendo projetado. Lembre-se, Z é um valor negativo no espaço da câmera.

![](../../attachments/Pasted%20image%2020260603074803.png)

Consideraremos a vista superior (plano XZ). O cenário forma dois triângulos retângulos semelhantes. Pela semelhança dos triângulos (catetos precisam ser valores positivos):
$$\frac{X^{\prime}}{-d}=\frac{X}{-Z}$$
Reorganizando a equação para encontrar a coordenada projetada $X^{\prime}$ (o eixo Y segue a mesma lógica):
$$X^{\prime}=\frac{X\cdot d}{Z}$$

Quanto maior a profundidade $(|Z|)$, menor será o valor projetado $(|X^{\prime}|)$, simulando o encolhimento de objetos distantes.

De acordo com o Teorema de Tales, se o plano de projeção estiver em $Z_{proj}=d$, as coordenadas projetadas $(X^{\prime},Y^{\prime},Z^{\prime})$ de um ponto $P(X,Y,Z)$ são:

$$X^{\prime}=\frac{X\cdot d}{Z} \text{ [cite: 217]}$$

$$Y^{\prime}=\frac{Y\cdot d}{Z} \text{ e } Z^{\prime}=d \text{[cite: 218].}$$

Para simplificar o cálculo da matriz, o plano de projeção padrão $d=-1$ é adotado. Assim, $X^{\prime}=\frac{X\cdot(-1)}{Z}=\frac{X}{-Z}$ $Y^{\prime}=\frac{Y\cdot(-1)}{Z}=\frac{Y}{-Z}$ $Z^{\prime}=-1$.

**Coordenadas Homogêneas**

Para representar a divisão por -Z (que é uma operação não-linear), deve-se usar coordenadas homogêneas. O elemento divisor deve ser movido para a coordenada homogênea $W^{\prime}$ (o último componente do vetor coluna).

$$P^{\prime}=\begin{pmatrix}X^{\prime}\\ Y^{\prime}\\ Z^{\prime}\\ 1\end{pmatrix}=\begin{pmatrix}X/(-Z)\\ Y/(-Z)\\ -1\\ 1\end{pmatrix}\cdot(-Z)=\begin{pmatrix}X\\ Y\\ Z\\ -Z\end{pmatrix} \quad M_{persp}^{singular}=\begin{pmatrix}1&0&0&0\\ 0&1&0&0\\ 0&0&1&0\\ 0&0&-1&0\end{pmatrix} \text{ [cite: 223]}$$

A matriz $M_{persp}$ representa a divisão por -Z ao colocar o valor 1 na posição $M_{4,3}$.

**Mapeamento Z com $\alpha$ e $\beta$**

Note que a matriz obtida acima é singular. Entretanto, para não perder a informação de profundidade dos vértices, deve-se usar uma matriz não-singular (determinante $\ne0$). Além de não perder essa informação, o mapeamento de profundidade deve alinhar os planos de corte near e far aos planos de corte correspondentes do CCV (1 e -1).

A terceira linha (Z) da matriz é a responsável por mapear o intervalo $[-f,-n]$ para o $Z_{ccv}\in[-1,1]$. Como o mapeamento de profundidade só depende da profundidade original $Z_{cam}$, os elementos $M_{3,1}$ e $M_{3,2}$ podem continuar zerados. $X_{cam}$ e $Y_{cam}$ não influenciam o $Z_{ccv}$ porque os planos de corte near e far não são inclinados, são alinhados aos eixos da câmera. Mas os outros 2 elementos, ainda desconhecidos, serão representados pelos coeficientes $\alpha$ e $\beta$.

**Derivação de $\alpha$ e $\beta$**

$$M_{persp}=\begin{pmatrix}1&0&0&0\\ 0&1&0&0\\ 0&0&\alpha&\beta\\ 0&0&-1&0\end{pmatrix} \text{ [cite: 233]}$$

Usando a nova matriz $M_{persp}$, a coordenada Z após a transformação, mas antes da divisão, é $Z^{\prime}=\alpha Z_{cam}+\beta$ Após a divisão por $W^{\prime}=-Z_{cam}$ a coordenada Z no CCV é:

$$Z_{ccv}=\frac{\alpha Z_{cam}+\beta}{-Z_{cam}}=-\alpha-\frac{\beta}{Z_{cam}} \text{[cite: 235].}$$

Aplicando as condições de contorno $(Z_{cam}=-n\rightarrow1 \text{ e } Z_{cam}=-f\rightarrow-1)$:

$Z_{cam} = -n \rightarrow Z_{ccv} = 1$: (Eq. 1) $1 =-\alpha-\frac{\beta}{-n}=-\alpha+\frac{\beta}{n}$ $Z_{cam} = -f \rightarrow Z_{ccv} = -1$: (Eq. 2) $-1=-\alpha-\frac{\beta}{-f}=-\alpha+\frac{\beta}{f}$

Resolvendo o sistema linear (subtraindo Eq. 2 de Eq. 1):

$$2=\frac{\beta}{n}-\frac{\beta}{f}=\beta\left(\frac{1}{n}-\frac{1}{f}\right)=\beta\frac{f-n}{fn} \text{ [cite: 241]}$$

Logo, $\beta=\frac{2fn}{f-n}$ . Substituindo na Eq. 1 para encontrar $\alpha$:

$$\alpha=\frac{\beta}{n}-1=\frac{2fn}{n(f-n)}-1=\frac{2f}{f-n}-1=\frac{2f-(f-n)}{f-n}=\frac{f+n}{f-n} \text{ [cite: 243]}$$

Resolvendo o sistema, obtemos:

$$\alpha=\frac{f+n}{f-n} \text{ e } \beta=\frac{2fn}{f-n} \text{ [cite: 245]}$$

**Importância da Preparação: Mapeamento de X e Y**

As transformações de Cisalhamento $(M_{shear})$ e Escala $(S_{ang})$ simplificam a matriz de perspectiva e garantem que, após a divisão homogênea, as faces inclinadas (laterais, superior e inferior) do frustum já estejam mapeadas corretamente para as faces do CCV $(X_{ccv}=\pm1 \text{ e } Y_{ccv}=\pm1)$.

Encaixe das Bordas: A combinação $S_{ang}\cdot M_{shear}$ transforma o frustum arbitrário (l, r, b, t) em um frustum simétrico canônico, em que as bordas já estão alinhadas com os $90^{\circ}$ de campo de visão. Ou seja, as bordas (faces inclinadas) laterais desse frustum simétrico canônico passam exatamente nos planos diagonais verticais, em que as coordenadas x são iguais às coordenadas z em módulo. Já nas bordas superior e inferior, as coordenadas y são iguais às coordenadas z em módulo. Assim, os planos de corte laterais, superior e inferior já se encaixam nas faces $X_{ccv}=\pm1$ e $Y_{ccv}=\pm1$ do CCV:

- • Para qualquer vértice na face lateral direita (r), $X=-Z$ Substituindo na fórmula $X_{ccv}=\frac{X}{-Z}$ o resultado fica $\frac{-z}{-z}=1$.
    
- • Para qualquer vértice na face lateral esquerda (l), $X=Z$ Substituindo na fórmula $X_{ccv}=\frac{X}{-Z}$ o resultado fica $\frac{z}{-z}=-1$.
    
- • Para qualquer vértice na face superior (t), $Y=-Z$ Substituindo na fórmula $Y_{ccv}=\frac{Y}{-Z}$ o resultado fica $\frac{-z}{-z}=1$.
    
- • Para qualquer vértice na face inferior (b), $Y=Z$. Substituindo na fórmula $Y_{ccv}=\frac{Y}{-Z}$ o resultado fica $\frac{z}{-z}=-1$.
    

Isso torna a primeira e a segunda linhas da matriz $M_{persp}$ simples, focando apenas no mapeamento de Z:

$$M_{persp}=\begin{pmatrix}1&0&0&0\\ 0&1&0&0\\ 0&0&\alpha&\beta\\ 0&0&-1&0\end{pmatrix} \text{ [cite: 259]}$$

**Simplificação da Derivação**

Em princípio, a transformação completa poderia ser realizada em uma única matriz $(sem~M_{shear} \text{ e } S_{ang})$, mas isso exigiria a introdução de coeficientes adicionais nas linhas X e Y, como $\beta_{x}$, $\alpha_{y}$ $\beta_{y}$:

$$P^{\prime}=\begin{pmatrix}\alpha_{x}X+\beta_{x}Z\\ \alpha_{y}Y^{\prime}+\beta_{y}Z\\ \alpha Z+\beta\\ -Z\end{pmatrix} \text{ [cite: 262]}$$

Aplicar as condições de contorno adequadas para gerar e resolver novos sistemas lineares, a fim de calcular esses coeficientes adicionais, pode ser considerado menos intuitivo. O uso das etapas preparatórias garante que, após $S_{ang}\cdot M_{shear}$, os coeficientes necessários para X e Y na matriz $M_{persp}$ se reduzam a $\alpha_{x}=1$ $\beta_{x}=0$, $\alpha_{y}=1$ e $\beta_{y}=0$ Isso simplifica o processo de derivação.


#### **3.4 Matriz final**
$$M_{fratum}=\begin{pmatrix}\frac{2n}{r-l}&0&\frac{l+r}{r-l}&0\\ 0&\frac{2n}{t-b}&\frac{b+t}{t-b}&0\\ 0&0&\frac{f+n}{f-n}&\frac{2fn}{f-n}\\ 0&0&-1&0\end{pmatrix}$$
