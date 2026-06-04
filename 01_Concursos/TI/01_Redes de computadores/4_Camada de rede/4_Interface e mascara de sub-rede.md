
#Concluded 

---
### **1. Interfaces**

Um hospedeiro em geral tem apenas um único enlace com a rede. <mark style="background: #ADCCFFA6;">A fronteira entre o hospedeiro e o enlace físico é denominada interface. </mark>

Considere um roteador e suas interfaces. Como a tarefa de um roteador é receber um datagrama em um enlace e repassá-lo a algum outro, ele necessariamente estará ligado a dois ou mais enlaces. Assim, um roteador tem **múltiplas interfaces.** 

Como todos os hospedeiros e roteadores podem enviar e receber datagramas IP, o IP exige que cada interface tenha seu próprio endereço. Desse modo, <mark style="background: #ADCCFFA6;">um endereço IP está tecnicamente associado com uma interface enão a um dispositivo.</mark>

Cada interface em cada hospedeiro da Internet global tem de ter um endereço IP exclusivo. Uma <mark style="background: #ADCCFFA6;">parte do endereço IP de uma interface será determinada pela sub-rede à qual ela está conectada e a outra parte referente a própria interface.</mark>

![Pasted image 20250524113525](../../../../attachments/Pasted%20image%2020250524113525.png)

---
### **2. Máscara de sub-rede**

**Sub-rede** é definida como um conjunto de interfaces de rede que são interconectadas e que compartilham uma parte comum do endereço IP. 

**Máscara de sub-rede** é um conceito utilizado para identificar qual parte de um endereço IP representa a sub-rede e qual parte identifica a interface dentro dessa sub-rede. A máscara de sub-rede é um número de 32 bits. A regra é:
- Bits `1` na máscara = **Endereço da Rede**.
- Bits `0` na máscara = **Endereço do Host**.
    
O computador faz uma operação lógica **AND** bit a bit entre o Endereço IP e a Máscara de Sub-rede. O resultado dessa operação é sempre o **ID da Rede**.

>[!EXAMPLE]
>- IP do seu PC: 192.168.1.100
>- Máscara de Sub-rede: 255.255.255.0
> 
|                 | **Em Binário**                                        |
| --------------- | ----------------------------------------------------- |
| **IP**          | `11000000.10101000.00000001.01100100`                 |
| **Máscara**     | `11111111.11111111.11111111.00000000`                 |
| **ID da Rede** | `11000000.10101000.00000001.00000000` = `192.168.1.0` |
Isso diz ao seu computador: Você está na rede 192.168.1.0. Qualquer IP que comece com 192.168.1 está na mesma sub-rede. 

---
### **3. CIDR (Classless InterDomain Routing)** 

A CIDR é apenas uma forma mais curta de escrever a máscara. Em vez de escrever o número 255.255.255.0 inteiro, o CIDR simplesmente conta quantos bits 1 existem na máscara.
- Na nossa máscara `255.255.255.0`, quantos bits `1` temos?   24  
- Portanto, a máscara `255.255.255.0` é escrita como **/24**, o prefixo de sub-rede.

**O que 223.1.1.0/24  nos diz?**

1. De um total de 32 bits, os primeiros 24 bits são o "prefixo da sub-rede" e os  8 bits restantes são para os Hosts.
    
2. **ID da Rede:** O endereço da rede é 223.1.1.0. 223.1.1 são fixos para todos nessa rede.
    
3. **Bits de Host:** Os 8 bits restantes são a parte que pode mudar para identificar os dispositivos.
    
4. **Capacidade da Rede:** Com 8 bits de host, temos $2^8 = 256$ endereços possíveis.
	- `223.1.1.0` O primeiro endereço é reservado como o endereço da rede.
	- `223.1.1.1-254` Hosts utilizaveis
	- `223.1.1.255` O último endereço é reservado como o endereço de broadcast para a subrede.

