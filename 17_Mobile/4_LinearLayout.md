
#Concluded 

---
O LinearLayout é um dos `ViewGroups` mais fundamentais. Sua função é organizar todos os elementos filhos em uma única direção (horizontal ou vertical)
![500](../attachments/Pasted%20image%2020260316144349.png)
![](../attachments/Pasted%20image%2020260316145502.png)

---
### **1. Atributos de espaço ocupado**
Para controlar como os elementos são organizados, você utiliza os seguintes atributos XML:

1. `android:orientation=vertical/horizontal `: Define a direção

2. `android:layout_width` e `android:layout_height=`: Define largura e altura.

3. `android:layout_weight`: O weight define quanto do espaço disponível um elemento deve ocupar proporcionalmente aos outros. Se você tem dois elementos com layout_weight="1", cada um ocupará 50% da largura. É recomendável definir a dimensão correspondente como 0dp. 
	![](../attachments/Pasted%20image%2020260316145752.png)
	![](../attachments/Pasted%20image%2020260316145704.png)


---
### **2. Padding e Margin**
Assim como no desenvolvimento web, margin e padding adicionam espaço dentro do elemento ou fora dele.
![280](../attachments/Pasted%20image%2020260316150735.png)
![](../attachments/Pasted%20image%2020260316150756.png)
![](../attachments/Pasted%20image%2020260316150658.png)

---
### **3. Gravity**
O atributo **gravity** define como o conteúdo de uma View deve ser posicionado dentro de seus próprios limites.

![](../attachments/Pasted%20image%2020260316152254.png)

O atributo **layout_gravity** define como a própria View deve se posicionar em relação ao seu pai. No LinearLayout, o layout_gravity só funciona no eixo oposto à orientação do layout:
![](../attachments/Pasted%20image%2020260316153028.png)

---
### **4. Visibility**

O atributo visibility controla a presença de uma View na interface e, crucialmente, como ela afeta o cálculo de layout dos outros elementos ao seu redor.

1. visible: A View é renderizada normalmente.
2. invisible: A View fica transparente, mas ela ainda ocupa o espaço destinado a ela no layout.
3. gone: A View não é renderizada e não ocupa espaço nenhum. 

![](../attachments/Pasted%20image%2020260316153603.png)