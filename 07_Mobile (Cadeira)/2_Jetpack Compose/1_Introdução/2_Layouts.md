
#Concluded 

--- 
Existem basicamente 3 layouts em jetpack componentes: Column, row and box. Como o Compose não sabe onde colocar os elementos por padrão, você usa esses três "containers" para organizar o layout.

![](../../../attachments/Pasted%20image%2020260318063308.png)

---
### **1. Row**

Recebe como parâmetros:
- **modifier**
- **verticalAlignment**: Controla o posicionamento no Eixo Secundário.
- **horizontalArrangement**
![400](../../../attachments/1_F0263XxPbXpoA9XdVL2mIw.gif)


![](../../../attachments/Pasted%20image%2020260318092916.png)
![](../../../attachments/Pasted%20image%2020260318093128.png)

---
### **2 Column**

Ele recebe como parâmetros:
- **modifier**
- **horizontalAlignment**: Controla o posicionamento no Eixo secundário.
- **verticalArrangement**: Controla o posicionamento no Eixo Principal.

![300](../../../attachments/1_AcweX3i0odfh9hJp2kI6hA.gif)
![](../../../attachments/Pasted%20image%2020260318094231.png)
![200](../../../attachments/Pasted%20image%2020260318094250.png)

---
### **3. Box** 

Contêiner responsável pelo alinhamento no Eixo Z (profundidade). Ele é utilizado para sobrepor elementos visuais. A renderização ocorre na exata ordem de declaração no código-fonte.

Parâmetros principais:
- **modifier**
- **contentAlignment**: Controla o posicionamento padrão de todos os elementos contidos no contêiner (por exemplo, centralizado, no canto inferior direito, etc.).

Modificadores exclusivos para os elementos filhos de um Box:
- **align()**: Permite que um componente filho específico ignore e sobrescreva o alinhamento geral definido pelo parâmetro `contentAlignment` do pai.
- **matchParentSize()**: Instrui o componente filho a igualar suas dimensões ao tamanho do Box pai, mas somente após o pai ter seu tamanho final definido pelos outros elementos do layout. 

![](../../../attachments/Pasted%20image%2020260506081512.png)
Um Box principal foi declarado para agrupar dois componentes distintos. A LazyRow foi o primeiro elemento declarado, estabelecendo-se na camada inferior. Logo após, um Box responsável por aplicar o gradiente de cor. 

A utilização da instrução matchParentSize() garantiu que a máscara possuísse exatamente a mesma altura e largura da LazyRow.
![](../../../attachments/mascarabox.gif)

**Surface**: O Surface é um contêiner focado exclusivamente na aplicação de propriedades físicas e visuais.

Parâmetros principais:
- **color**: Estabelece a cor de fundo da superfície do contêiner.
- **contentColor**: Configura a cor base padronizada para componentes de tipografia (Text e Icon). Este comportamento visa garantir um nível de contraste e legibilidade adequados em relação à cor de fundo.
- **shape**: Define a forma geométrica do contêiner, permitindo a aplicação de bordas específicas, como cantos arredondados. 
- **shadowElevation / tonalElevation**: Adicionam propriedades físicas de elevação ao componente, gerando projeções de sombras ou ajustando a opacidade da cor para destacá-lo no eixo de profundidade.