#Concluded 

---
### **1. Interfaces**

Um hospedeiro em geral tem apenas um único enlace com a rede; quando o IP no hospedeiro quer enviar um datagrama, ele o faz por meio desse enlace. **A fronteira entre o hospedeiro e o enlace físico é denominada interface**. 

Considere um roteador e suas interfaces. Como a tarefa de um roteador é receber um datagrama em um enlace e repassá-lo a algum outro, ele necessariamente estará ligado a dois ou mais enlaces.  Assim, um roteador tem múltiplas interfaces. 

Como todos os hospedeiros e roteadores podem enviar e receber datagramas IP, o IP exige que cada interface tenha seu próprio endereço. Desse modo, **um endereço IP está tecnicamente associado com uma interface**.

Cada interface em cada hospedeiro e roteador da Internet global tem de ter um endereço IP  exclusivo.  Uma parte do endereço IP de uma interface será determinada pela sub-rede à qual ela está conectada e a outra parte referente a própria interface.

![Pasted image 20250524113525](../../attachments/Pasted%20image%2020250524113525.png)

==Cada endereço IPv4 tem comprimento de 32 bits (equivalente a 4 bytes).==

---
### **2 Máscara de sub-rede**

Uma **sub-rede** é definida como um conjunto de interfaces de rede que são interconectadas e que compartilham uma parte comum do endereço IP. 

**Máscara de sub-rede** é um conceito utilizado para identificar qual parte de um endereço IP representa a sub-rede e qual parte identifica o dispositivo dentro dessa sub-rede. 
#### **2.1 CIDR (Classless InterDomain Routing)**
- **A porção da rede:** O CIDR permite que a porção de rede tenha tamanho variável entre entre 0 e 32 bits.
- **Formato do endereço: ==a.B.C.D/x==
    - **a.B.C.D:** é o endereço IP.
    - **/x:** é a máscara de rede em notação de prefixo, indicando quantos bits compõem a porção de rede do endereço.

No exemplo `223.1.1.0/24`, os primeiros 24 bits são o **prefixo da sub-rede**, e os 8 bits restantes servem para identificar os hosts.

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
    - É comum em servidores, impressoras de rede, roteadores e outros dispositivos que precisam ter um endereço IP fixo e conhecido para serem acessados de forma consistente.

2. **DHCP (Dynamic Host Configuration Protocol): **
	- Método **mais recomendado** para a maioria dos dispositivos em uma rede
    - **Como funciona:**
        - Quando um host se conecta a uma rede configurada com DHCP, ele envia uma solicitação para encontrar um servidor DHCP.
        - O servidor DHCP, oferece um endereço IP disponível do seu pool, juntamente com outras informações de configuração de rede (máscara de sub-rede, gateway, etc.).
        - O host aceita configura sua interface de rede com os parâmetros recebidos.
        - Os endereços IP são alocados por um **período de tempo limitado**. Antes que o tempo expire, o host tenta renovar o endereço com o servidor DHCP.

---

### Atribuição de Endereços (DHCP)

Um dispositivo não vem com um IP pré-definido. Ele precisa solicitar um endereço ao se conectar à rede.

- **DHCP (Dynamic Host Configuration Protocol):** É o protocolo usado para a atribuição automática de endereços IP em uma rede.
    
- **Processo:**
    
    1. Quando seu dispositivo (ex: laptop) se conecta à LAN (via Wi-Fi ou cabo), ele envia uma mensagem de _DHCP Request_ (um "broadcast" para a rede local) pedindo um endereço.
        
    2. O **Roteador**, que geralmente atua como o **Servidor DHCP** da rede, recebe essa solicitação.
        
    3. O roteador seleciona um endereço IP disponível de um "pool" (intervalo) pré-configurado e o oferece ao dispositivo.
        
    4. Junto com o IP, ele também fornece informações críticas de configuração, como a **Subnet Mask** (Máscara de Sub-rede) e o **Default Gateway** (Gateway Padrão, que é o endereço IP do próprio roteador).
        

### Tópico 4: Tradução de Endereços (NAT)

O vídeo aborda um ponto crucial: o seu laptop e o seu celular podem ter o mesmo IP (`192.168.1.100`) que o laptop do seu vizinho. Isso funciona devido à divisão entre IPs públicos e privados.

- **Endereços IP Privados:** São blocos de endereços não roteáveis na internet, reservados para uso em redes locais (LANs). Exemplos comuns são os blocos `192.168.x.x` ou `10.x.x.x`. Seu roteador atribui esses IPs aos _seus_ dispositivos.
    
- **Endereço IP Público:** É o **único** endereço IP que seu ISP (provedor) atribui ao seu modem/roteador. Este é o seu endereço visível para a Internet global.
    
- **NAT (Network Address Translation):** É o processo que o roteador executa para permitir que múltiplos dispositivos (com IPs privados) compartilhem um único IP público.
    
    - **Saída:** Quando seu laptop (`192.168.1.100`) acessa um site, o roteador "traduz" o pacote: ele troca o IP de origem privado pelo seu IP público.
        
    - **Entrada:** Quando o site responde ao IP público, o roteador consulta sua "tabela NAT", lembra qual dispositivo privado fez a solicitação original e traduz o IP de destino de volta para `192.168.1.100`.
        

### Tópico 5: Resolução de Nomes (DNS)

Os usuários não digitam endereços IP para acessar sites, eles usam nomes de domínio (hostnames) como `google.com`.

- **DNS (Domain Name System):** É o protocolo hierárquico e distribuído responsável por traduzir nomes de domínio legíveis por humanos em endereços IP roteáveis.
    
- **Processo de Resolução:**
    
    1. O usuário digita `google.com` no navegador.
        
    2. O sistema operacional envia uma consulta DNS para um **Servidor DNS** (geralmente fornecido via DHCP pelo seu ISP, ou um público como `8.8.8.8` do Google).
        
    3. O servidor DNS responde à consulta com o endereço IP público correspondente ao `google.com` (ex: `172.217.14.228`).
        
    4. Com o IP de destino em mãos, o navegador pode então iniciar a conexão.
        

---

Aperte `next` para o próximo tópico, que aborda como os dados são realmente enviados (TCP) e como vários aplicativos usam a mesma conexão (Portas).