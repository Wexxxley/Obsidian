

---

**A) O produto escalar entre dois vetores ortogonais é igual a zero.**

 $\vec{u} \cdot \vec{v} = \|\vec{u}\| \|\vec{v}\| \cos(\theta)$. Quando dois vetores são ortogonais, o ângulo entre eles é exatamente $90^\circ$. Como o cosseno de $90^\circ$ é  $0$, a multiplicação inteira resulta em $0$.

**B) Considerando que o produto vetorial entre dois vetores é igual ao vetor nulo, podemos dizer que eles são paralelos.**

A magnitude do vetor resultante de um produto vetorial é dada pela equação $\|\vec{u} \times \vec{v}\| = \|\vec{u}\| \|\vec{v}\| \sin(\theta)$. Para que o resultado seja o vetor nulo, a condição necessária é que o termo $\sin(\theta)$ seja igual a zero. 

**C) A distância entre os pontos $P_1 = (-1, 3, -2)$ e $P_2 = (-2, 4, -2)$ é igual a $\sqrt{2}$.**

A distância entre dois pontos é calculada pela raiz quadrada da soma dos quadrados das diferenças de suas coordenadas correspondentes:
$$d = \sqrt{(-2 - (-1))^2 + (4 - 3)^2 + (-2 - (-2))^2}$$
$$d = \sqrt{(-1)^2 + (1)^2 + (0)^2}$$
$$d = \sqrt{1 + 1 + 0}$$
$$d = \sqrt{2}$$


**D) A multiplicação entre duas matrizes consiste em uma série de produtos escalares entre as linhas da primeira matriz e as colunas da segunda matriz.**

Esses dois conjuntos de números são tratados como vetores, e a operação realizada entre eles é exatamente o produto escalar: multiplica-se o primeiro elemento da linha pelo primeiro da coluna, o segundo pelo segundo, e assim por diante, somando-se todos os resultados parciais para obter um único valor numérico (um escalar) para aquela posição específica da matriz resultante.

**E) A multiplicação de uma matriz ortonormal por um vetor coluna à sua direita pode ser interpretada tanto como uma combinação linear das colunas da matriz quanto como uma projeção do vetor coluna nas linhas da matriz.**

Existem duas formas primárias de interpretar a multiplicação de uma matriz por um vetor coluna $\vec{v}$.

Na primeira visão (focada nas colunas), o vetor resultante é uma combinação linear das colunas da matriz. 

Na segunda visão (focada nas linhas), cada elemento do vetor resultante é calculado realizando o produto escalar entre uma linha da matriz e o vetor coluna $\vec{v}$. Quando a matriz é ortonormal (suas linhas formam uma base de vetores perpendiculares entre si e de comprimento 1), o produto escalar calcula rigorosamente a projeção ortogonal do vetor $\vec{v}$ sobre a direção definida por aquela linha específica.

**F) Ao transformar o sistema de coordenadas local de um objeto, as coordenadas globais dos seus vértices mudam, enquanto as coordenadas locais dos seus vértices se mantêm inalteradas.**

Na Computação Gráfica, as coordenadas locais são definidas em relação à origem do próprio objeto. Elas descrevem a geometria intrínseca da malha 3D.

Quando aplicamos uma transformação ao sistema de coordenadas local do objeto, estamos movendo o objeto pelo mundo virtual. No entanto, a estrutura do objeto em si não é deformada; portanto, a distância e a posição dos vértices em relação ao centro do próprio objeto (suas coordenadas locais) permanecem estritamente inalteradas.


----

**A) A inversa de uma matriz de escala é igual a sua transposta.**

**Resposta:** ( F ) Falso. A matriz transposta de uma matriz de escala (que é uma matriz diagonal) é exatamente igual à matriz original ($S^T = S$). Por outro lado, a inversa de uma matriz de escala contém os inversos multiplicativos dos fatores de escala originais na sua diagonal principal (por exemplo, se o fator de escala de $x$ é 2, na inversa será 1/2). A propriedade de ter a inversa igual à transposta ($M^{-1} = M^T$) é exclusiva de matrizes ortogonais, como as matrizes de rotação.

**2. As coordenadas homogêneas são necessárias para possibilitar a representação de transformações de rotação e escala através de matrizes, permitindo que elas possam ser combinadas.**

**Resposta:** ( F ) Falso. As transformações de rotação e de escala são transformações estritamente lineares e já podem ser plenamente representadas e combinadas usando matrizes comuns $3 \times 3$ no espaço 3D (ou $2 \times 2$ em 2D). O real motivo para a introdução das coordenadas homogêneas (aumentando a matriz para $4 \times 4$) é a necessidade de representar a **translação** como uma multiplicação de matrizes. 

**3. Na matriz de conversão de um sistema global para um sistema local, o $R^T$ que multiplica o -t é responsável por converter -t de coordenadas globais para coordenadas locais.**

**Resposta:** ( V ) Verdadeiro. A transformação do espaço local para o global de uma câmera ou objeto é dada por $M = T \cdot R$. Para converter do global de volta para o local, precisamos da matriz inversa $M^{-1} = (T \cdot R)^{-1} = R^{-1} \cdot T^{-1}$. Como $R$ é uma matriz ortogonal, sua inversa é sua transposta ($R^T$). O inverso da translação é o deslocamento oposto $T(-t)$. Portanto, $M^{-1} = R^T \cdot T(-t)$. Geometricamente, as linhas da matriz de rotação transposta $R^T$ representam os eixos do sistema de coordenadas local. Ao multiplicar $R^T$ pelo vetor global de translação $-t$, estamos fazendo o produto escalar desse vetor com os eixos locais, o que o projeta e o converte efetivamente para o espaço de coordenadas local.

**4. O produto vetorial entre um vetor qualquer p e um vetor unitário u equivale geometricamente à projeção do vetor p sobre o vetor u.**

**Resposta:** ( F ) Falso.

**Justificativa:** A operação geométrica descrita no enunciado corresponde ao **produto escalar** (dot product), e não ao produto vetorial. O produto escalar entre um vetor $\vec{p}$ e um vetor unitário $\vec{u}$, representado por $\vec{p} \cdot \vec{u}$, resulta em um escalar que quantifica exatamente a magnitude da projeção ortogonal de $\vec{p}$ sobre $\vec{u}$. O produto vetorial (cross product), por sua vez, resultaria em um novo vetor perpendicular tanto a $\vec{p}$ quanto a $\vec{u}$.

**5. A rotação de -60 graus ao redor do eixo x de um ponto (x,y,z) altera apenas suas coordenadas y e z.**

**Resposta:** ( V ) Verdadeiro.

**Justificativa:** Em uma operação de rotação 3D ao redor de um eixo canônico, as coordenadas pertencentes a esse eixo funcionam como o pivô da transformação e permanecem completamente inalteradas. A matriz de rotação em torno do eixo $x$ aplica funções trigonométricas (senos e cossenos do ângulo de -60 graus) exclusivamente sobre os outros dois eixos, promovendo um giro no plano ortogonal $yz$. Assim, a coordenada $x$ original do ponto é preservada, enquanto apenas $y$ e $z$ mudam.


---

A matriz de transformação $T$ representa uma rotação seguida de uma translação. 
$$T = M_T \cdot M_R = \begin{bmatrix} I & t \\ 0 & 1 \end{bmatrix} \begin{bmatrix} R & 0 \\ 0 & 1 \end{bmatrix} = \begin{bmatrix} R & t \\ 0 & 1 \end{bmatrix}$$
$$T^{-1} = M_R^{-1} \cdot M_T^{-1}$$
- **Inversa da Rotação:** a sua inversa é igual à sua transposta.
$$M_R^{-1} = \begin{bmatrix} R^T & 0 \\ 0 & 1 \end{bmatrix}$$
- **Inversa da Translação:**    $$M_T^{-1} = \begin{bmatrix} I & -t \\ 0 & 1 \end{bmatrix}$$
- **Inversa de T**
$$T^{-1} = \begin{bmatrix} R^T & 0 \\ 0 & 1 \end{bmatrix} \begin{bmatrix} I & -t \\ 0 & 1 \end{bmatrix}$$
$$T^{-1} = \begin{bmatrix} R^T & -R^T t \\ 0 & 1 \end{bmatrix}$$

$-t$  representa o vetor de deslocamento para a posição original. $R^T$, converte o vetor de deslocamento (que estava no eixo do mundo) para o sistema de coordenadas rotacionado do objeto. 
