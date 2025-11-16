

---
### **1. Como um ISP obtém seu bloco de endereço?**

- **ICANN (Internet Corporation for Assigned Names and Numbers):** A ICANN é a autoridade global máxima responsável por coordenar a atribuição de identificadores únicos na Internet. 

- **RIRs (Regional Internet Registries):** A ICANN delega a alocação de grandes blocos de endereços IP para cinco RIRs, que cobrem diferentes regiões do mundo:
    
    1. A **ICANN** aloca grandes blocos de endereços IP para cada **RIR**.
    2. Um **ISP** em uma determinada região solicita um bloco de endereços IP à sua **RIR**
    3. A **RIR** avalia a necessidade do ISP e aloca um bloco de endereços.
    4. O ISP então usa esse bloco para atribuir endereços IP a seus clientes 

---
### **2. Atribuição de enderços IP**

1. **Definido pelo administrador do sistema:**    
    - Neste método, o endereço IP, a máscara de sub-rede, o gateway padrão e os servidores DNS são **manualmente inseridos** nas configurações de rede do host.

2. **DHCP (Dynamic Host Configuration Protocol):** É o protocolo usado para a atribuição automática de endereços IP em uma rede.
    
    1. Quando seu dispositivo se conecta à LAN, ele envia uma mensagem de _DHCP Request_ ("broadcast" para a rede local) pedindo um endereço.
        
    2. O Roteador, que geralmente atua como o Servidor DHCP da rede, recebe essa solicitação. Ele seleciona um endereço IP disponível de um intervalo pré-configurado e o oferece ao dispositivo.
        
    3. Junto com o IP, ele também fornece a **Subnet Mask** (Máscara de Sub-rede) e o **Default Gateway** (Gateway Padrão, que é o endereço IP do próprio roteador).

