

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

F) Ao transformar o sistema de coordenadas local de um objeto, as coordenadas **globais** dos seus vértices mudam, enquanto as coordenadas **locais** dos seus vértices se mantêm inalteradas.

Na Computação Gráfica, as coordenadas locais são definidas em relação à origem do próprio objeto. Elas descrevem a geometria intrínseca da malha 3D.

Quando aplicamos uma transformação ao sistema de coordenadas local do objeto, estamos movendo o objeto pelo mundo virtual. No entanto, a estrutura do objeto em si não é deformada; portanto, a distância e a posição dos vértices em relação ao centro do próprio objeto (suas coordenadas locais) permanecem estritamente inalteradas.

### Item G: Armazenamento e carregamento de modelos 3D

**Enunciado:** Ao salvar um objeto tridimensional em um arquivo, seus vértices são salvos em coordenadas **locais**. Ao carregar o arquivo, suas coordenadas **globais** são obtidas automaticamente através de uma matriz de composição de transformações.

**Explicação:** Quando um software de modelagem 3D exporta um arquivo (como `.obj` ou `.fbx`), a geometria é salva utilizando coordenadas locais. Isso garante que o objeto seja modular e independente, podendo ser instanciado múltiplas vezes em uma cena sem conflitos de posicionamento.

Ao carregar esse arquivo em um motor gráfico, o objeto precisa ser posicionado no cenário. Para isso, o motor lê as coordenadas locais e as multiplica por uma matriz de composição de transformações (frequentemente chamada de Matriz de Modelo ou _Model Matrix_). O resultado dessa multiplicação converte os dados brutos do arquivo nas coordenadas globais, estabelecendo onde e como o objeto existe dentro do espaço do mundo virtual simulado.