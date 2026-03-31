
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
### **3. Estado vs Variável comum**

- **Variável Comum:** Se você altera o valor de uma variável local comum, o valor muda na memória, mas a UI não sabe disso. Ela continua exibindo o valor antigo.
    
- **Variável de Estado:** Quando você altera um estado, o framework detecta essa mudança e dispara automaticamente o processo de Recomposição. 

- **Variável Comum:** Toda vez que a função do componente é executada novamente, a variável comum é reinicializada com seu valor padrão. 
    
- **Variável de Estado:** Através de mecanismos como o remember, o framework reserva um espaço na memória permitindo que o valor seja lembrado.