
#Concluded 

---
### **1. Base**

Para um conjunto de vetores ser considerado uma base de um espaço $V$, ele precisa obrigatoriamente cumprir duas condições:
1. Tem que serem **linearmente independentes.**
2. Combinando esses vetores, você deve ser capaz de alcançar qualquer ponto dentro do espaço vetorial $V$.

Na matemática aplicada à computação gráfica, um espaço vetorial tridimensional é definido por uma base u, v, w. Eles definem as três direções fundamentais do espaço.

Os objetos não existem em um único sistema de coordenadas. Um modelo 3D é criado em seu próprio sistema local, chamado de Espaço do Objeto. Para que a cena seja renderizada, este modelo precisa ser posicionado no mundo e, em seguida, avaliado a partir do ponto de vista de uma câmera virtual.

### **2. Mudança de Base**

A mudança de base é a operação matemática que converte as coordenadas de um vértice descritas em um sistema (como o do objeto) para as coordenadas equivalentes em outro sistema (como o do mundo).

A matriz de mudança de base $M$ que transforma pontos do sistema local para o sistema global é construída posicionando os vetores da base local como as colunas da matriz:
$$ M = \begin{bmatrix} u_x & v_x & w_x \\ u_y & v_y & w_y \\ u_z & v_z & w_z \end{bmatrix} $$

Se tivermos um ponto $\mathbf{p}_{local}$ no espaço do objeto, a sua posição no espaço do mundo é obtida multiplicando a matriz $M$ pelo vetor coluna $\mathbf{p}_{local}$:
$$ \mathbf{p}_{world} = M \cdot \mathbf{p}_{local} $$
Para permitir que a matriz aplique a translação, o espaço tridimensional é expandido matematicamente para o sistema de Coordenadas Homogêneas. A matriz de mudança de base se torna uma matriz $4 \times 4$. Sendo $O_x, O_y, O_z$ as coordenadas globais do ponto de origem do sistema local: 
$$ M = \begin{bmatrix} u_x & v_x & w_x & O_x \\ u_y & v_y & w_y & O_y \\ u_z & v_z & w_z & O_z \\ 0 & 0 & 0 & 1 \end{bmatrix} $$
O vértice a ser transformado é extraído. Suas coordenadas $(x, y, z)$ são convertidas em um vetor coluna de coordenadas homogêneas.
$$ \mathbf{p}_{local} = \begin{bmatrix} x \\ y \\ z \\ 1 \end{bmatrix} $$
$$ \mathbf{p}_{global} = M \cdot \mathbf{p}_{local} $$
Muitas vezes, é necessário realizar o caminho inverso. Para isso, utiliza-se a matriz inversa, denotada por $M^{-1}$.
$$ \mathbf{p}_{local} = M^{-1} \cdot \mathbf{p}_{world} $$


