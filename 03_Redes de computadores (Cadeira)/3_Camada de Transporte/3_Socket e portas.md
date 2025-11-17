
#Concluded 

---
### **1. Socket e porta**

**Porta**: Número (0 - 65.535) que serve para identificar qual processo está usando uma conexão dentro de um computador.
- O endereço IP leva até o computador.
- A porta diz qual o programa em execução que vai enviar ou receber algo.

**Socket**: Combinação de um Endereço IP e um Número de Porta(`172.217.14.228:443`). As portas permitem que o TCP ou UDP (Transporte) entregue os dados ao aplicativo correto, enquanto o IP (Rede) os entrega ao computador correto.

**Exemplo**: Digamos que você está acessando um site. A conexão é feita assim:
1. Seu navegador cria um socket local com:
	- IP da sua máquina e Porta aleatória local.
2. E se conecta a um socket remoto com:
	- IP do servidor e Porta do serviço.  
3. Esse par ==(local IP, local porta, remoto IP, remoto porta)== identifica  a conexão.

---
### **2. Programação com sockets**

#### **Socket UDP (Sem Conexão)**: 
Um socket UDP é identificado por dois valores: IP de destino e Porta de destino.  
![500](../../attachments/Pasted%20image%2020250509132053.png)

#### **Socket TCP (com  Conexão):** 
Um socket TCP é identificado por quatro valores: IP de origem, Porta de origem, IP de destino e Porta de destino.  

![500](../../attachments/Pasted%20image%2020250509132033.png)
