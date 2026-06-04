
#Concluded 

---
#### **1. Unicast (Um para Um)**
Um pacote é enviado de um **único remetente** para um **único receptor.
	![500](../../../../attachments/Pasted%20image%2020251215164918.png)
	
#### **2. Broadcast (Um para Todos/difusão)**
A comunicação Broadcast é quando um pacote é enviado de um **único remetente** para **todos os dispositivos** dentro de um domínio de broadcast específico.

- Quando um pacote broadcast é enviado, **todos os dispositivos** (incluindo os não roteadores) na mesma sub-rede recebem e precisam **processar** esse pacote até um certo ponto para determinar se ele é relevante para eles. 
	![500](../../../../attachments/Pasted%20image%2020251215165025.png)
 - **Ex:** Cliente DHCP envia um broadcast para encontrar um servidor DHCP na rede.

#### **3. Multicast (Um para Muitos Selecionados)**
A comunicação Multicast é quando um pacote é enviado de um **único remetente** para um **grupo de receptores específicos** que manifestaram interesse em receber essa informação.

- Os dispositivos que desejam receber o tráfego Multicast precisam se "inscrever" em um grupo Multicast específico.

- Com multicast, os dispositivos que **não fazem parte do grupo multicast** podem ignorar o pacote em um nível muito mais baixo da pilha de protocolos. 
	![500](../../../../attachments/Pasted%20image%2020251215165243.png)

#### **4. Anycast (Um para Um "Mais Próximo")**
O mesmo endereço IP é atribuído a **múltiplos dispositivos** (servidores) em diferentes localizações. Quando um cliente envia um pacote para esse endereço Anycast, a rede o roteia para o **servidor "mais próximo"**
	![500](../../../../attachments/Pasted%20image%2020251215165434.png)