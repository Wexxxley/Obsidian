
#Concluded 

---
### **1. Interfaces**

Um hospedeiro em geral tem apenas um único enlace com a rede. <mark style="background: #ADCCFFA6;">A fronteira entre o hospedeiro e o enlace físico é denominada interface. </mark>

Considere um roteador e suas interfaces. Como a tarefa de um roteador é receber um datagrama em um enlace e repassá-lo a algum outro, ele necessariamente estará ligado a dois ou mais enlaces. Assim, um roteador tem **múltiplas interfaces.** 

Como todos os hospedeiros e roteadores podem enviar e receber datagramas IP, o IP exige que cada interface tenha seu próprio endereço. Desse modo, <mark style="background: #ADCCFFA6;">um endereço IP está tecnicamente associado com uma interface enão a um dispositivo.</mark>

Cada interface em cada hospedeiro da Internet global tem de ter um endereço IP exclusivo. Uma <mark style="background: #ADCCFFA6;">parte do endereço IP de uma interface será determinada pela sub-rede à qual ela está conectada e a outra parte referente a própria interface.</mark>

![Pasted image 20250524113525](../../attachments/Pasted%20image%2020250524113525.png)

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
| >**ID da Rede** | `11000000.10101000.00000001.00000000` = `192.168.1.0` |
Isso diz ao seu computador: Você está na rede 192.168.1.0. Qualquer IP que comece com 192.168.1 está na mesma sub-rede. 

**CIDR (Classless InterDomain Routing)**: A CIDR é apenas uma forma mais curta de escrever a máscara. Em vez de escrever o número 255.255.255.0 inteiro, o CIDR simplesmente conta quantos bits 1 existem na máscara.
- Na nossa máscara `255.255.255.0`, quantos bits `1` temos?   24  
- Portanto, a máscara `255.255.255.0` é escrita como **/24**, o prefixo de sub-rede.

**O que 223.1.1.0/24  nos diz?**

1. De um total de 32 bits, os primeiros 24 bits são o "prefixo da sub-rede" e os  8 bits restantes são para os Hosts.
    
2. **ID da Rede:** O endereço da rede é 223.1.1.0. 223.1.1 são fixos para todos nessa rede.
    
3. **Bits de Host:** Os 8 bits restantes (o último número, `.0`) são a parte que pode mudar para identificar os dispositivos.
    
4. **Capacidade da Rede:** Quantos dispositivos cabem nessa rede? Com 8 bits de host, temos $2^8 = 256$ endereços possíveis.
    

**Os 256 endereços são:**

- `223.1.1.0` (o primeiro endereço, todos os 8 bits de host são `0`). Este é reservado como o **endereço da rede**.
    
- `223.1.1.1` (o primeiro host utilizável).
    
- ... (passando por `223.1.1.2`, `223.1.1.3` ...)
    
- `223.1.1.254` (o último host utilizável).
    
- `223.1.1.255` (o último endereço, todos os 8 bits de host são `1`). Este é reservado como o **endereço de broadcast** (para "falar" com todos na rede de uma vez).
    

**Conclusão:** O endereço `223.1.1.0/24` descreve uma rede que contém 256 endereços, indo de `223.1.1.0` até `223.1.1.255`.



---
### **3. Endereços IP reservados**

**1. Endereço Local**: Comunicação interna dentro da máquina. Como em testar servidores locais.
- **Faixa**: `127.0.0.0/8` (o mais usado é `127.0.0.1`)

**2. Endereço de Rede**: Identifica a própria **sub-rede**, não pode ser atribuído a um host.
- **Característica**: Todos os bits da porção de host são **0**.

**3. O endereço de broadcast:** O último endereço da sub-rede (onde todos os bits de host são um).
- O endereço de broadcast é um endereço IP especial que serve para **enviar uma mensagem a _todos_ os dispositivos dentro _daquela sub-rede específica_**.

**4. Endereços Privados:** Reservados para redes internas (não são roteáveis pela Internet pública).

---
### **4. Como um ISP obtém seu bloco de endereço?**

- **ICANN (Internet Corporation for Assigned Names and Numbers):**
    1. A ICANN é a autoridade global máxima responsável por coordenar a atribuição de identificadores únicos na Internet. 
- **RIRs (Regional Internet Registries):** A ICANN delega a alocação de grandes blocos de endereços IP para cinco RIRs, que cobrem diferentes regiões do mundo:
    - **AFRINIC:** África
    - **APNIC:** Ásia/Pacífico
    - **ARIN:** América do Norte
    - **LACNIC:** América Latina e Caribe (onde o Brasil se encaixa)
    - **RIPE NCC:** Europa, Oriente Médio e partes da Ásia Central
    
    1. A **ICANN** aloca grandes blocos de endereços IP para cada **RIR**.
    2. Um **ISP** em uma determinada região solicita um bloco de endereços IP à sua **RIR**
    3. A **RIR** avalia a necessidade do ISP e aloca um bloco de endereços.
    4. O ISP então usa esse bloco para atribuir endereços IP a seus clientes 

---
### **5. Atribuição de enderços IP**

1. **Definido pelo administrador do sistema:**    
    - Neste método, o endereço IP, a máscara de sub-rede, o gateway padrão e os servidores DNS são **manualmente inseridos** nas configurações de rede do host.

2. **DHCP (Dynamic Host Configuration Protocol):** É o protocolo usado para a atribuição automática de endereços IP em uma rede.
    
    1. Quando seu dispositivo se conecta à LAN, ele envia uma mensagem de _DHCP Request_ ("broadcast" para a rede local) pedindo um endereço.
        
    2. O Roteador, que geralmente atua como o Servidor DHCP da rede, recebe essa solicitação. Ele seleciona um endereço IP disponível de um intervalo pré-configurado e o oferece ao dispositivo.
        
    3. Junto com o IP, ele também fornece a **Subnet Mask** (Máscara de Sub-rede) e o **Default Gateway** (Gateway Padrão, que é o endereço IP do próprio roteador).

