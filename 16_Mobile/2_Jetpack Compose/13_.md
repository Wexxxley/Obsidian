

---
O Jetpack Compose transforma estados em elementos da UI da seguinte forma:
![](../../attachments/Pasted%20image%2020260324065138.png)
#### **1. Composition**
Na fase de composição, as funções @Composable são executas gerando uma estrutura em árvore que representa a interface.
![550](../../attachments/Pasted%20image%2020260324065327.png)
#### **2. Layout**
Durante esta fase, a árvore de UI é percorrida. Os nós da árvore possuem as informações necessárias para decidir o tamanho e a localização de cada um. Ao final dessa etapa, cada nó sabe sua posição e seu tamanho.

Passos do algoritmo:
1. Medir largura e altura dos filhos se houver.
2. Com base nisso, um nó decide o próprio tamanho.
3. Posicionar filhos em relação ao pai.

![300](../../attachments/Pasted%20image%2020260324070053.png)
#### **3. Drawing**
A árvore é percorrida novamente, mas dessa vez, como os elementos estão posicionados basta ir aplicando os design de cada nó.
![400](../../attachments/Pasted%20image%2020260324070216.png)

