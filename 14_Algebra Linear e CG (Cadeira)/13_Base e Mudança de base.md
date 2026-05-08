
#Concluded 

---
### **1. Base**

Para um conjunto de vetores ser considerado uma base de um espaço $V$, ele precisa obrigatoriamente cumprir duas condições:
1. Tem que serem **linearmente independentes.**
2. Combinando esses vetores, você deve ser capaz de alcançar qualquer ponto dentro do espaço vetorial $V$.

Na matemática aplicada à computação gráfica, um espaço vetorial tridimensional é definido por uma "base". Uma base é um conjunto de três vetores (frequentemente denotados como $\mathbf{u}$, $\mathbf{v}$ e $\mathbf{w}$ para o 3d). Eles definem as três direções fundamentais do espaço.

Qualquer ponto ou vetor dentro desse espaço pode ser expresso como uma combinação linear desses vetores base. Se temos um vetor $\mathbf{p}$, suas coordenadas $(x, y, z)$ representam os coeficientes que multiplicam cada vetor da base para alcançar a posição no espaço:
$$ \mathbf{p} = x\mathbf{u} + y\mathbf{v} + z\mathbf{w} $$

Pglobal = Blocal * Plocal
Plocal = Blocal⁻1 * Pglobal

Os objetos não existem em um único sistema de coordenadas. Um modelo 3D é criado em seu próprio sistema local, chamado de Espaço do Objeto (Object Space). Para que a cena seja renderizada, este modelo precisa ser posicionado no mundo (World Space) e, em seguida, avaliado a partir do ponto de vista de uma câmera virtual (Camera Space).

A mudança de base é a operação matemática que converte as coordenadas de um vértice descritas em um sistema (como o do objeto) para as coordenadas equivalentes em outro sistema (como o do mundo).

Seja a base local do objeto definida pelos vetores ortonormais (vetores de comprimento igual a $1$ e perpendiculares entre si) $\mathbf{u}$, $\mathbf{v}$ e $\mathbf{w}$, cujas coordenadas são conhecidas em relação ao sistema global do mundo. A matriz de mudança de base $M$ que transforma pontos do sistema local para o sistema global é construída posicionando os vetores da base local como as colunas da matriz:
$$ M = \begin{bmatrix} u_x & v_x & w_x \\ u_y & v_y & w_y \\ u_z & v_z & w_z \end{bmatrix} $$

Se tivermos um ponto $\mathbf{p}_{local}$ com coordenadas $(x, y, z)$ no espaço do objeto, a sua posição no espaço do mundo, $\mathbf{p}_{world}$, é obtida multiplicando a matriz $M$ pelo vetor coluna $\mathbf{p}_{local}$:
$$ \mathbf{p}_{world} = M \cdot \mathbf{p}_{local} $$

Para permitir que a matriz aplique a translação, o espaço tridimensional é expandido matematicamente para um espaço tetradimensional (sistema de Coordenadas Homogêneas).

A matriz de mudança de base se torna uma matriz $4 \times 4$. Sendo $O_x, O_y, O_z$ as coordenadas globais do ponto de origem do sistema local, a matriz completa de transformação do espaço local para o global é expressa como:
$$ M = \begin{bmatrix} u_x & v_x & w_x & O_x \\ u_y & v_y & w_y & O_y \\ u_z & v_z & w_z & O_z \\ 0 & 0 & 0 & 1 \end{bmatrix} $$
O vértice a ser transformado é extraído. Suas coordenadas $(x, y, z)$ são convertidas em um vetor coluna de coordenadas homogêneas.
$$ \mathbf{p}_{local} = \begin{bmatrix} x \\ y \\ z \\ 1 \end{bmatrix} $$
$$ \mathbf{p}_{global} = M \cdot \mathbf{p}_{local} $$
Muitas vezes, é necessário realizar o caminho inverso. Para isso, utiliza-se a matriz inversa, denotada por $M^{-1}$.

$$ \mathbf{p}_{local} = M^{-1} \cdot \mathbf{p}_{world} $$

