
---

### **1. Endereço MAC/LAN/FÍSICO**
- Usado para levar o datagrama de uma interface física a outra na mesma rede.
- Endereços MAC tem 48 bits. Cada placa de rede no mundo possui seu proprio end físico e é gravado na memória fixa ROM do adaptador.
- A alocação de endereços MAC é administrada pelo IEEE, os fabricantes podem comprar porções do espaço de endereço MAC. 
- Endereçamento MAC possui **portabilidade**, ou seja, sua máquina pode ter o mesmo end MAC mesmo em redes diferentes. Para isso, não pode ter duas máquinas com o mesmo end físico.
- Se for preciso mudar o end MAC, os drivers podem omitir o end da ROM e usam outro.

---
### **2. ARP (Address Resolution Protocol)** 

Protocolo usado para **descobrir o endereço MAC de um dispositivo a partir do endereço IP.**

Imagine que seu computador (A) quer enviar um pacote de dados para outro computador (B) na mesma rede local. O dispositivo A sabe o **endereço IP** do Dispositivo B. No entanto, para que o pacote seja entregue, o dispositivo A precisa saber o **endereço MAC** do Dispositivo B.

Cada Nó IP (Host, Roteador) numa LAN tem um módulo e uma tabela ARP

- **Módulo ARP**: Componente de software responsável por executar as operações do prot ARP.
- **Tabela ARP**: Cada nó mantém uma **Tabela ARP**. Que é uma lista de mapeamentos entre endereços IP e seus correspondentes endereços MAC.

	![Pasted image 20250627115140](../../attachments/Pasted%20image%2020250627115140.png)

	- **`Time To Live)`**: O **Tempo de Vida** para aquela entrada na tabela, tipicamente 20 min.

- **ARP Request - Broadcast**: Quando um dispositivo precisa descobrir um endereço MAC para um IP que não está em sua tabela, ele pergunta para _todos_ na rede local. 
- **ARP Reply - Unicast**: O dispositivo que possui o endereço IP alvo recebe a requisição. Como ele agora sabe o endereço MAC do remetente, ele pode enviar a **Resposta ARP** diretamente.

- Cada porta (interface) de um roteador que está conectada a uma LAN diferente funciona como um "nó IP" independente. Portanto, se um roteador tem, por exemplo, três interfaces de rede, ele terá **uma tabela ARP separada para CADA UMA dessas interfaces de LAN ativas**.

---
### **3. Pacote ARP** 

![Pasted image 20250627120308](../../attachments/Pasted%20image%2020250627120308.png)

- **Tipo de Hardware**: Indica o tipo de hardware da rede em que o ARP está operando. Por exemplo, `1` para Ethernet.
- **Tipo de Protocolo**: Especifica o protocolo da Camada de Rede.
- **Tamanho do Endereço Físico**: O número de bytes do endereço MAC.
- **Tamanho do Protocolo**: O número de bytes do endereço de protocolo. 
- **Operação (Solicitação 1, Resposta 2)**:
    - `1`: É uma **Requisição ARP**: O remetente está perguntando "Quem tem este IP?".
    - `2`: É uma **Resposta ARP**: O remetente está respondendo "Eu tenho este IP"
- **Endereço Físico de Origem**: O endereço MAC do dispositivo que está enviando o pacote ARP.
- **Protocolo do Endereço de Origem**: O endereço IP do dispositivo que está enviando o pacote.
- **Endereço Físico de Destino**: So preenchido na resposta.

**Quadro de resposta**

![Pasted image 20250627120715](../../attachments/Pasted%20image%2020250627120715.png)

- **Preâmbulo**
    - Usado para sincronizar os relógios do transmissor e do receptor.
- **Endereço de Destino**:
    - Em uma **Requisição ARP**: Este campo é **FFFFFFFFFFFF**, que é o **end de broadcast MAC**.
    - Em uma **Resposta ARP**: Este campo é o end MAC do dispositivo que fez a Requisição.
- **Endereço de Origem**: O endereço MAC do dispositivo que está enviando o quadro.
- **Tipo**: Este campo indica qual protocolo da camada superior está encapsulado nos "Dados".
- **Dados**: Esta é a área onde o **Pacote ARP** ou IP é inserido.
- **CRC**: Basicamente um checksum

---

### **4_MAC fora da rede local**

Máquina A (na Rede 1) Quer Falar com Máquina B (na Rede 2)

1. **A cria o pacote IP com origem A, destino B.**
    - A máquina A, ao verificar o endereço IP de destino, percebe que B _não está na mesma rede. 
    - A cria um quadro com destino para seu  **gateway padrão**. 
2. **O roteador recebe o quadro**        
    - O roteador verifica o endereço MAC de destino. Como é o seu próprio, ele aceita.
    - O roteador desencapsula o quadro. Ele agora tem o **datagrama IP.
    - O roteador examina o **endereço IP de destino**. Ele consulta sua **tabela de roteamento**. A tabela de roteamento dirá por qual de suas interfaces o pacote deve sair.
    - O roteador envia uma Requisição ARP na rede de destino perguntando: "Quem tem o IP de B?". A máquina B responde com seu endereço MAC.    
    - Com o endereço MAC, o roteador R agora cria um **novo quadro**. O **endereço MAC de destino** deste _novo_ quadro será o MAC da máquina **B**. O **endereço MAC de origem** será o MAC da interface do próprio roteador roteador.