

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

A projeção perspectiva (cônica) transforma o frustum de visualização (tronco de pirâmide) no Cubo Canônico de Visualização (CCV). Essa transformação é mais complexa, pois envolve a divisão por $-Z_{cam}$ (coordenadas homogêneas) para criar o efeito de perspectiva e, para simplificação, uma série de transformações preparatórias.

A matriz final de normalização da projeção perspectiva ($M_{frustum}$) é uma composição de três etapas principais:

$$M_{frustum}=M_{persp}\cdot S_{ang}\cdot M_{shear}$$

- $M_{shear}$ Cisalhamento para tornar o frustum simétrico (centro em $X=0,Y=0$).
    
- $S_{ang}:$ Escala para normalizar os ângulos de abertura, ajustando o tamanho da face frontal para a dimensão padrão de $2n\times2n$.
    
- $M_{persp}$: Matriz que aplica a lógica da perspectiva (Divisão por Z) e o mapeamento de Z ($\alpha~e~\beta$).
    

Nota sobre Mapeamento Z: Mapeamento adotado: $Z_{cam}=-n\rightarrow1~e~Z_{cam}=-f\rightarrow-1$.

### 4.1 Cisalhamento ($M_{shear}$): Tornando o Frustum Simétrico

O glFrustum permite que o plano near ($Z_{cam}=-n$) seja assimétrico, ou seja, $\frac{l+r}{2}|\ne0$ e $|\frac{b+t}{2}|\ne0$. O objetivo do cisalhamento é deslocar o centro do retângulo do plano near de $|\begin{matrix}\#\\ \frac{l+r}{2},&\#\\ (\frac{l+r}{2}\end{matrix}|\begin{matrix}\#\\ 2\end{matrix}|$ para (0,0). O deslocamento necessário, em $X_{cam}e~Y_{cam}$ é proporcional a $Z_{cam}$.

- **Fator de Cisalhamento $sh_{x}$**: O deslocamento necessário em $X_{cam}$ no plano near é $-\frac{l+r}{2}$. Usando a expressão algébrica $X^{\prime}=X+sh_{x}\cdot Z$ e sabendo que o centro $X=\frac{l+r}{2}$ deve ir para $X^{\prime}=0$ no plano $Z=-n:$
    
    $$j=\frac{l+r}{2}+sh_{x}\cdot(-n)\Rightarrow sh_{x}=\frac{-\frac{l+r}{2}}{-n}=\frac{l+r}{2n}$$
    
- **Fator de Cisalhamento $sh_{y}$**: Analogamente, $sh_{y}=\frac{b+t}{2n}$.
    

O cisalhamento é dado por:

$$M_{shour}=\begin{pmatrix}1&0&sh_{x}&0\\ 0&1&sh_{y}&0\\ 0&0&1&0\\ 0&0&0&1\end{pmatrix}=\begin{pmatrix}1&0&\frac{l+x}{2t_{1}}&0\\ 0&1&\frac{l+x}{2n}&0\\ 0&0&1&0\\ 0&0&0&1\end{pmatrix}$$

### 4.2 Escala ($S_{ang}$): Ajuste Angular ($90^{\circ}$)

Após o cisalhamento, temos um frustum simétrico, mas com largura e altura no plano near de r-let-b, respectivamente. A escala $S_{ang}$ é aplicada para que as novas dimensões do frustum no plano near sejam $2n\times2n$. Este ajuste garante que o frustum seja normalizado como se tivesse um campo de visão de $90^{\circ}$.

- **Fator de Escala $S_{x}$**: A largura atual ($r-l$) deve ser ajustada para 2n. Logo, $S_{x}=\frac{2n}{r-l}.$
    
- **Fator de Escala $S_{y}$**: A altura atual ($t-b$) deve ser ajustada para 2n. Logo, $S_{y}=\frac{2n}{t-b}$
    

$$S_{ang}=\begin{pmatrix}\frac{2n}{r-1}&0&0&0\\ 0&\frac{2n}{r-b}&0&0\\ 0&0&1&0\\ 0&0&0&1\end{pmatrix}$$

**Relação entre o campo de visão de $90^{\circ}$ e as novas dimensões $2n\times2n$**

Em uma visão ortográfica lateral, a pirâmide com as novas dimensões $2n\times2n$ no plano near apareceria cortada pelo eixo Z, dividindo seu ângulo de abertura vertical de $90^{\circ}$ em 2 ângulos de $45^{\circ}$ e formando 2 triângulos retângulos com o plano near. Como esses triângulos retângulos possuem 2 ângulos de $45^{\circ}$, seus catetos também precisam ter o mesmo tamanho ($b^{\prime}=-n$ $t^{\prime}=n$). Em uma visão ortográfica superior, de maneira análoga, $l^{\prime}=-n$ -ner $r^{\prime}=n$.

### 4.3 Matriz de Perspectiva ($M_{persp}$)

A matriz $M_{persp}$ finaliza a transformação do frustum simétrico normalizado para o CCV, aplicando a lógica da perspectiva e o mapeamento de profundidade. O encaixe das bordas (faces inclinadas: laterais, superior e inferior) do frustum nas bordas do CCV também funciona devido aos ajustes prévios de cisalhamento e escala.

**Projeção Perspectiva e o Teorema de Tales**

O Teorema de Tales (ou semelhança de triângulos) é o princípio geométrico fundamental que governa a projeção perspectiva, explicando porque a divisão pela profundidade Z é necessária.

O cenário da projeção perspectiva envolve três elementos-chave, que formam um triângulo retângulo na vista superior (ou lateral):

- **Observador (Câmera)**: Localizado na origem (0,0,0).
    
- **Plano de Projeção (Imagem)**: Localizado em uma distância d do observador. No nosso sistema de câmera (onde o observador olha para-Z), o plano está em $Z_{proj}=d$ (onde dé negativo, e.g., $d=-1$).
    
- **Ponto na Cena (P)**: Um ponto $P(X,Y,Z)$ que está sendo projetado. Lembre-se, Zé um valor negativo no espaço da câmera.
    

Consideraremos a vista superior (plano XZ). O cenário forma dois triângulos retângulos semelhantes:

- Triângulo Grande é formado pelo ponto na cena $P(X,Y,Z)$, a origem (câmera), e o eixo Z.
    
- O Triângulo Pequeno é formado pelo ponto projetado $P^{\prime}(X^{\prime},Y^{\prime},d)$ no plano de projeção, a origem, e o plano de projeção em $Z_{proj}=d$.
    

Pela semelhança dos triângulos (catetos precisam ser valores positivos):

$$\frac{X^{\prime}}{-d}=\frac{X}{-Z}$$

Reorganizando a equação para encontrar a coordenada projetada $X^{\prime}$ (o eixo Y segue a mesma lógica):

$$X^{\prime}=\frac{X\cdot d}{Z}$$

Esta fórmula demonstra que a coordenada projetada é inversamente proporcional à profundidade (Z). Quanto maior a profundidade $(|Z|)$, menor será o valor projetado $(|X^{\prime}|)$, simulando o encolhimento de objetos distantes.

**Da Álgebra à Matriz**

De acordo com o Teorema de Tales, se o plano de projeção estiver em $Z_{proj}=d$, as coordenadas projetadas $(X^{\prime},Y^{\prime},Z^{\prime})$ de um ponto $P(X,Y,Z)$ são:

$X^{\prime}=\frac{X\cdot d}{Z}$, $Y^{\prime}=\frac{Y\cdot d}{Z}$ e $Z^{\prime}=d$.

Para simplificar o cálculo da matriz, o plano de projeção padrão $d=-1$ é adotado. Assim, $X^{\prime}=\frac{X\cdot(-1)}{Z}=\frac{X}{-Z}$, $Y^{\prime}=\frac{Y\cdot(-1)}{Z}=\frac{Y}{-Z}$ e $Z^{\prime}=-1$.

**Coordenadas Homogêneas**

Para representar a divisão por -Z (que é uma operação não-linear), deve-se usar coordenadas homogêneas. O elemento divisor deve ser movido para a coordenada homogênea $W^{\prime}$ (o último componente do vetor coluna).

$$P^{\prime}=\begin{pmatrix}X^{\prime}\\ Y^{\prime}\\ Z^{\prime}\\ 1\end{pmatrix}=\begin{pmatrix}X/(-Z)\\ Y/(-Z)\\ -1\\ 1\end{pmatrix}\cdot(-Z)=\begin{pmatrix}X\\ Y\\ Z\\ -Z\end{pmatrix}$$

$$M_{presp}^{simguiar}=\begin{pmatrix}1&0&0&0\\ 0&1&0&0\\ 0&0&1&0\\ 0&0&-1&0\end{pmatrix}$$

A matriz $M_{persp}$ representa a divisão por -Z ao colocar o valor 1 na posição $M_{4,3}$.

**Mapeamento Z com $\alpha~e~\beta$**

Note que a matriz obtida acima é singular. Entretanto, para não perder a informação de profundidade dos vértices, deve-se usar uma matriz não-singular (determinante $\ne0$). Além de não perder essa informação, o mapeamento de profundidade deve alinhar os planos de corte near e far aos planos de corte correspondentes do CCV $(1~e-1)$.

A terceira linha (Z) da matriz é a responsável por mapear o intervalo $[-f,-n]$ para o $Z_{ccv}\in[-1,1]$. Como o mapeamento de profundidade só depende da profundidade original $Z_{cam}$, os elementos $M_{3,1}e~M_{3,2}$ podem continuar zerados. $X_{cam}e~Y_{cam}$ não influenciam o $Z_{cGt}$ porque os planos de corte near e far não são inclinados, são alinhados aos eixos da câmera. Mas os outros 2 elementos, ainda desconhecidos, serão representados pelos coeficientes $\alpha~e~\beta$.

**Derivação de $\alpha$ e $\beta$**

$$M_{prrap}=\begin{pmatrix}1&0&0&0\\ 0&1&0&0\\ 0&0&\alpha&\beta\\ 0&0&-1&0\end{pmatrix}$$

Usando a nova matriz $M_{persp}$, a coordenada Z após a transformação, mas antes da divisão, é $Z^{\prime}=\alpha Z_{cam}+\beta$. Após a divisão por $W^{\prime}=-Z_{cam}$ a coordenada Z no CCV é:

$$Z_{ccv}=\frac{\alpha Z_{cam}+\beta}{-Z_{cam}}=-\alpha-\frac{\beta}{Z_{cam}}.$$

Aplicando as condições de contorno $(Z_{cam}=-n\rightarrow1$ $Z_{cam}=-f\rightarrow-1)$:

- Zcam = -nZccv = 1: (Eq. 1) $1 =-\alpha-1=-\alpha+\beta$ _(correção da notação conforme contexto do pdf)_
    
- Zcam = -f Zeev = -1: (Eq. 2) $-1=-\alpha-4-1=-\alpha+\beta$
    

Resolvendo o sistema linear (subtraindo Eq. 2 de Eq. 1):

$$2=\frac{\beta}{n}-\frac{\beta}{f}=\beta(\frac{1}{n}-\frac{1}{f})=\beta\frac{f-n}{fn}$$

Logo, $\beta=\frac{2fn}{f-n}$. Substituindo na Eq. 1 para encontrar a:

$$\alpha=\frac{\beta}{n}-1=\frac{2fn}{n(f-n)}-1=\frac{2f}{f-n}-1=\frac{2f-(f-n)}{f-n}=\frac{f+n}{f-n}$$

Resolvendo o sistema, obtemos:

$\alpha=\frac{f+n}{f-n}e~\beta=\frac{2fn}{f-n}$

**Importância da Preparação: Mapeamento de X e Y**

As transformações de Cisalhamento $(M_{shear})$ e Escala $(S_{ang})$ simplificam a matriz de perspectiva e garantem que, após a divisão homogênea, as faces inclinadas (laterais, superior e inferior) do frustum já estejam mapeadas corretamente para as faces do CCV $(X_{ccv}=\pm1~e~Y_{ccv}=\pm1)$.

Encaixe das Bordas A combinação $S_{ang}\cdot M_{shear}$ transforma o frustum arbitrário $(l,r,b,t)$ em um frustum simétrico canônico, em que as bordas já estão alinhadas com os $90^{\circ}$ de campo de visão. Ou seja, as bordas (faces inclinadas) laterais desse frustum simétrico canônico passam exatamente nos planos diagonais verticais, em que as coordenadas x são iguais às coordenadas z em módulo. Já nas bordas superior e inferior, as coordenadas y são iguais às coordenadas z em módulo. Assim, os planos de corte laterais, superior e inferior já se encaixam nas faces $X_{ccv}=\pm1$ e $Y_{ccv}=\pm1$ do CCV:

- Para qualquer vértice na face lateral direita (r), $\frac{X}{-Z}$ o resultado fica $\frac{-z}{-z}=1$, $X=-Z$. Substituindo na fórmula $X_{ccv}=$
    
- Para qualquer vértice na face lateral esquerda (1), $X=Z$, $\frac{X}{-Z}$ o resultado fica $\frac{z}{-z}=-1$.
    
- Para qualquer vértice na face superior (t), $Y=-Z$ Substituindo na fórmula $Y_{ccv}=\frac{Y}{-Z}$ resultado fica $\frac{-z}{-z}=1$.
    
- Para qualquer vértice na face inferior (b), $Y=Z$. Substituindo na fórmula $Y_{ccv}=\frac{Y}{-Z}$ resultado fica $\frac{z}{-z}=-1$.
    

Isso torna a primeira e a segunda linhas da matriz $M_{persp}$ simples, focando apenas no mapeamento de Z:

$$M_{persp}=\begin{pmatrix}1&0&0&0\\ 0&1&0&0\\ 0&0&\alpha&\beta\\ 0&0&-1&0\end{pmatrix}$$

**Simplificação da Derivação** Em princípio, a transformação completa poderia ser realizada em uma única matriz $(sem~M_{shear}e~S_{ang})$, mas isso exigiria a introdução de coeficientes adicionais nas linhas X e Y, como $\beta_{x}$, $\alpha_{y}$ $\beta_{y}$:

$$P^{\prime}=\begin{pmatrix}\alpha_{x}X+\beta_{x}Z\\ \alpha_{y}Y^{\prime}+\beta_{y}Z\\ \alpha Z+\beta\\ -Z\end{pmatrix}$$

Aplicar as condições de contorno adequadas para gerar e resolver novos sistemas lineares, a fim de calcular esses coeficientes adicionais, pode ser considerado menos intuitivo. O uso das etapas preparatórias garante que, após $S_{ang}\cdot M_{shear}$, os coeficientes necessários para X e Y na matriz $M_{persp}$ se reduzam a $\alpha_{x}=1$ $\beta_{x}=0$, $\alpha_{y}=1$ e $\beta_{y}=0$ Isso simplifica o processo de derivação.

### 4.4 Matriz Final $(M_{frustum})$

A matriz final $M_{frustum}$ combina $M_{persp}\cdot S_{ang}\cdot M_{shear}:$

$$M_{frustam}=\begin{pmatrix}1&0&0&0\\ 0&1&0&0\\ 0&0&\frac{l+n}{f-n}&\frac{2ln}{f-n}\\ 0&0&-1&0\end{pmatrix}\cdot\begin{pmatrix}\frac{2n}{r-i}&0&0&0\\ 0&\frac{2n}{r-i}&0&0\\ 0&0&1&0\\ 0&0&1&0\\ 0&0&1&0\\ 0&0&1\end{pmatrix}\cdot\begin{pmatrix}1&0&\frac{l+n}{2n}&0\\ 0&0&1&0\\ 0&0&1&0\\ 0&0&1\end{pmatrix}$$

$$M_{fratum}=\begin{pmatrix}\frac{2a}{r-1}&0&\frac{l+r}{r-l}&0\\ 0&\frac{2a}{r-l}&\frac{l+l}{r-l}&0\\ 0&0&\frac{l+m}{l-n}&\frac{2ln}{l-n}\\ 0&0&-1&0\end{pmatrix}$$

**Exemplo Numérico**

Parâmetros: $l=-1$, $r=1$, $b=-1$, $t=1$, $n=2$, $f=100$.

- Termos X e Y: $\frac{2(2)}{1-(-1)}=2$, $\frac{-1+1}{1-(-1)}=0$
    
- Termos $Z(\alpha~e~\beta);$: $\alpha=\frac{100+2}{100-2}=\frac{102}{98}\approx1.0408~\beta=\frac{2(100)(2)}{100-2}=\frac{400}{98}\approx4.0816.$
    

$$M_{frastum}=\begin{pmatrix}2&0&0&0\\ 0&2&0&0\\ 0&0&1.0408&4.0816\\ 0&0&-1&0\end{pmatrix}$$