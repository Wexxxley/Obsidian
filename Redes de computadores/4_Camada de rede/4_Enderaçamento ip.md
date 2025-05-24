

---

### **1.1 Interfaces**
Um hospedeiro em geral tem apenas um único enlace com a rede; quando o IP no hospedeiro quer enviar um datagrama, ele o faz por meio desse enlace. **A fronteira entre o hospedeiro e o enlace físico é denominada interface**. 

Agora considere um roteador e suas interfaces. Como a tarefa de um roteador é receber um datagrama em um enlace e repassá-lo a algum outro enlace, ele necessariamente estará ligado a dois ou mais enlaces. A fronteira entre o roteador e qualquer um desses enlaces também é denominada uma interface. Assim, um roteador tem múltiplas interfaces. Como todos os hospedeiros e roteadores podem enviar e receber datagramas IP, o IP exige que cada interface tenha seu próprio endereço IP. Desse modo, **um endereço IP está tecnicamente associado com uma interface**, e não com um hospedeiro 

![[Pasted image 20250524113525.png]]

==Cada endereço IPv4 tem comprimento de 32 bits (equivalente a 4 bytes).==

Cada interface em cada hospedeiro e roteador da Internet global tem de ter um endereço IP  exclusivo. Contudo, os endereços não podem ser escolhidos de qualquer maneira. Uma parte do endereço IP de uma interface será determinada pela sub-rede à qual ela está conectada.

---
### **1.2 Máscara de sub-rede**
**Sub-rede:** uma **sub-rede** é definida como um conjunto de interfaces de rede que são interconectadas e que compartilham uma parte comum do endereço IP. 

**máscara de sub-rede**: é um conceito utilizado para identificar qual parte de um endereço IP representa a sub-rede e qual parte identifica o dispositivo dentro dessa sub-rede. 

> O endereçamento IP designa um endereço a essa sub-rede: 223.1.1.0/24, no qual a notação /24 indica que os 24 bits mais à esquerda do conjunto de 32 bits definem o endereço da sub-rede e o restante do dispositivo.

Ou seja, no exemplo `223.1.1.0/24`, os primeiros 24 bits são o **prefixo da sub-rede**, e os 8 bits restantes servem para identificar os hosts.

A máscara de sub-rede pode ser representada também em formato decimal, por exemplo:
- `/24` → `255.255.255.0`
- `/16` → `255.255.0.0`

---
### **1.3 Endereços IP reservados**

**1. Endereço Local**
- **Faixa**: `127.0.0.0/8` (o mais usado é `127.0.0.1`)
- **Uso**: Comunicação interna dentro da própria máquina. Como em testar servidores locais sem sair da máquina.

 **2. Endereço de Rede**
- **Uso**: Identifica a própria **sub-rede**, não pode ser atribuído a um host.
- **Característica**: Todos os bits da porção de host são **0**.
- **Exemplo**: `192.168.1.0` (em uma sub-rede /24).

 **3. Endereço de Difusão (Broadcast)**
- **Uso**: Identifica as máquinas da rede 

 **4. Endereços Privados (RFC 1918)**
- Reservados para redes internas (não são roteáveis pela Internet pública).
    
- Faixas:
    
    - `10.0.0.0/8` (10.0.0.0 a 10.255.255.255)
        
    - `172.16.0.0/12` (172.16.0.0 a 172.31.255.255)
        
    - `192.168.0.0/16` (comum: `192.168.0.0/24`, `192.168.1.0/24`)
        
