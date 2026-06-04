
#Concluded 

---
### **1. Segmento tcp**

![Pasted image 20250509134237](../../../../attachments/Pasted%20image%2020250509134237.png)


---
### **2. Buffers de envio e de recepção**

![Pasted image 20250509133804](../../../../attachments/Pasted%20image%2020250509133804.png)

#### **2.1 Buffer de Envio**
Tem a função de armazenar dados que a aplicação quer enviar, mas que ainda não foram transmitidos (ou não foram confirmados pelo receptor).
#### **2.2 Buffer de Recepção**
Armazena dados recebidos da rede, mas ainda não lidos pela aplicação. 
**Se encher:** O TCP avisa o remetente para parar de enviar (controle de fluxo).
### **2.3 Janela Deslizante do TCP**
É um mecanismo que controla quantos dados podem ser enviados antes de receber uma confirmação (ACK). Usado no controle de fluxo do TCP.

1. **O receptor controla a janela deslizante**: Ele diz ao transmissor: _"Tenho espaço para X bytes no buffer"_ (via campo `Window Size` ).
2. **O transmissor obedece**: Só envia novos dados se couberem na janela atual. Se o buffer estiver cheio, ele espera até o receptor liberar espaço.
