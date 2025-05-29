

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
#### **1.2.1 CIDR (Classless InterDomain Routing)**
- **A porção da rede tem tamanho arbitrário:** Ao invés de ter tamanhos de rede fixos, o CIDR permite que a porção de rede (e, consequentemente, a porção de host) tenha qualquer tamanho entre 0 e 32 bits
- **Formato do endereço: `a.B.C.D/x`:** em que `x` é o número de bits na parte de rede do endereço.
    - `a.B.C.D` é o endereço IP, geralmente o endereço da rede.
    - `/x` é a máscara de rede em notação de prefixo, indicando quantos bits (contando da esquerda para a direita) compõem a porção de rede do endereço.

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

---


