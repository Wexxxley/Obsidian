
#Concluded 

---
### **1. Base**

Para um conjunto de vetores ser considerado uma base de um espaço $V$, ele precisa obrigatoriamente cumprir duas condições:
1. Tem que serem **linearmente independentes.**
2. Combinando esses vetores, você deve ser capaz de alcançar qualquer ponto dentro do espaço vetorial $V$.

![500](../attachments/20260312_191853029.jpg)


1. **A Base Canônica (World Space):** O mundo padrão que usamos tem os eixos perpendiculares usuais. $\hat{i} = (1, 0, 0)$, $\hat{j} = (0, 1, 0)$, $\hat{k} = (0, 0, 1)$.
2. **Uma Base Arbitrária (Local Space):** base local de um objeto.


3. **Espaço do Objeto:** O artista modela um objeto com o centro dela no $(0,0,0)$.
4. **World Space:** A cadeira é colocada na cena no ponto $(10, 0, 5)$ e rotacionada. Fazemos uma mudança de base para saber onde os vértices da cadeira estão no mundo.
5. **View Space:** O mundo inteiro é recalculado de forma que a câmera se torne a nova origem $(0,0,0)$, olhando diretamente para o eixo $-Z$.


Na matemática aplicada à computação gráfica, um espaço vetorial tridimensional é definido por uma "base". Uma base é um conjunto de três vetores (frequentemente denotados como $\mathbf{u}$, $\mathbf{v}$ e $\mathbf{w}$ para o 3d). Eles definem as três direções fundamentais do espaço.

Qualquer ponto ou vetor dentro desse espaço pode ser expresso como uma combinação linear desses vetores base. Se temos um vetor $\mathbf{p}$, suas coordenadas $(x, y, z)$ representam os coeficientes que multiplicam cada vetor da base para alcançar a posição final no espaço:

$$ \mathbf{p} = x\mathbf{u} + y\mathbf{v} + z\mathbf{w} $$

### A Necessidade da Mudança de Base na Computação Gráfica

Em um pipeline gráfico, os objetos não existem em um único sistema de coordenadas. Um modelo 3D é criado em seu próprio sistema local, chamado de Espaço do Objeto (Object Space). Para que a cena seja renderizada, este modelo precisa ser posicionado no mundo (World Space) e, em seguida, avaliado a partir do ponto de vista de uma câmera virtual (Camera Space ou View Space).

A mudança de base é a operação matemática que converte as coordenadas de um vértice descritas em um sistema (como o do objeto) para as coordenadas equivalentes em outro sistema (como o do mundo ou da câmera), preservando a integridade geométrica do modelo.

### A Matriz de Mudança de Base (Matriz de Transformação)

Para realizar a conversão matemática de um sistema de coordenadas $A$ para um sistema de coordenadas $B$, utilizamos a multiplicação de matrizes.

Seja a base local do objeto definida pelos vetores ortonormais (vetores de comprimento igual a $1$ e perpendiculares entre si) $\mathbf{u}$, $\mathbf{v}$ e $\mathbf{w}$, cujas coordenadas são conhecidas em relação ao sistema global do mundo. A matriz de mudança de base $M$ que transforma pontos do sistema local para o sistema global é construída posicionando os vetores da base local como as colunas da matriz:

$$ M = \begin{bmatrix} u_x & v_x & w_x \\ u_y & v_y & w_y \\ u_z & v_z & w_z \end{bmatrix} $$

Se tivermos um ponto $\mathbf{p}_{local}$ com coordenadas $(x, y, z)$ no espaço do objeto, a sua posição no espaço do mundo, $\mathbf{p}_{world}$, é obtida multiplicando a matriz $M$ pelo vetor coluna $\mathbf{p}_{local}$:

$$ \mathbf{p}_{world} = M \cdot \mathbf{p}_{local} $$

### Sistemas de Referência (Frames) e Coordenadas Homogêneas

A matriz $3 \times 3$ descrita acima permite a rotação e o redimensionamento, mas falha em um aspecto essencial: a translação. Na computação gráfica, os sistemas locais não possuem apenas direções (vetores base), mas também uma origem no espaço, formando o que chamamos formalmente de "Frame" ou sistema de referência afim.

Para permitir que a matriz aplique a translação (o deslocamento da origem local em relação à origem global), o espaço tridimensional é expandido matematicamente para um espaço tetradimensional. Isso é chamado de sistema de Coordenadas Homogêneas. Adicionamos uma quarta coordenada aos nossos vetores e pontos. Para pontos no espaço, essa quarta coordenada é $1$. Para vetores direcionais (que não possuem posição, apenas direção), a quarta coordenada é $0$.

A matriz de mudança de base se torna uma matriz $4 \times 4$. Sendo $O_x, O_y, O_z$ as coordenadas globais do ponto de origem do sistema local, a matriz completa de transformação do espaço local para o global é expressa como:

$$ M = \begin{bmatrix} u_x & v_x & w_x & O_x \\ u_y & v_y & w_y & O_y \\ u_z & v_z & w_z & O_z \\ 0 & 0 & 0 & 1 \end{bmatrix} $$

### Passo a Passo Matemático da Transformação

**Passo 1: Definição do Ponto de Origem**

O vértice a ser transformado é extraído de sua malha poligonal. Suas coordenadas $(x, y, z)$ são convertidas em um vetor coluna de coordenadas homogêneas, adicionando o valor $1$ na base.

$$ \mathbf{p}_{local} = \begin{bmatrix} x \\ y \\ z \\ 1 \end{bmatrix} $$

**Passo 2: Construção da Matriz de Transformação**

A matriz $M$ é preenchida com os vetores direcionais do objeto ($\mathbf{u}$, $\mathbf{v}$, $\mathbf{w}$) nas três primeiras colunas e a posição da origem geométrica do objeto no espaço global na quarta coluna.

**Passo 3: Produto Matricial**

Realiza-se o produto da matriz $4 \times 4$ pelo vetor $4 \times 1$. O cálculo algébrico para a nova coordenada $x'$ no espaço global, por exemplo, ocorre pela soma dos produtos dos elementos da primeira linha da matriz pelos elementos correspondentes do vetor coluna:

$$ x' = (u_x \cdot x) + (v_x \cdot y) + (w_x \cdot z) + (O_x \cdot 1) $$

Este procedimento é repetido para as linhas de $y'$, $z'$ e a quarta coordenada (que permanecerá $1$). O resultado é o novo vetor descrevendo exatamente o mesmo ponto, mas sob a perspectiva da base global.

### A Transformação Inversa

Muitas vezes, é necessário realizar o caminho inverso, como converter um ponto luminoso do espaço global para o espaço local do objeto (processo comum em cálculos de iluminação). Para isso, utiliza-se a matriz inversa, denotada por $M^{-1}$.

$$ \mathbf{p}_{local} = M^{-1} \cdot \mathbf{p}_{world} $$

No contexto estrito de bases ortonormais em computação gráfica (onde ocorre apenas rotação, sem distorção ou escala), a matriz inversa da parte rotacional ($3 \times 3$) é numericamente igual à sua matriz transposta (a inversão de linhas por colunas). Essa propriedade, denominada ortogonalidade da matriz, é amplamente explorada na arquitetura de software gráfico para otimizar o custo computacional, visto que transpor uma matriz exige um número consideravelmente menor de operações de ponto flutuante do que calcular a sua inversão completa através de métodos como a eliminação de Gauss.