
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
	![[Pasted image 20250627115140.png]]
	- **`Time To Live)`**: O **Tempo de Vida** para aquela entrada na tabela, tipicamente 20 min.

- **ARP Request - Broadcast**: Quando um dispositivo precisa descobrir um endereço MAC para um IP que não está em sua tabela, ele pergunta para _todos_ na rede local. 
- **ARP Reply - Unicast**: O dispositivo que possui o endereço IP alvo recebe a requisição. Como ele agora sabe o endereço MAC do remetente, ele pode enviar a **Resposta ARP** diretamente.

- Cada porta (interface) de um roteador que está conectada a uma LAN diferente funciona como um "nó IP" independente. Portanto, se um roteador tem, por exemplo, três interfaces de rede, ele terá **uma tabela ARP separada para CADA UMA dessas interfaces de LAN ativas**.

---
### **3. Pacote ARP** 

![[Pasted image 20250627120308.png]]

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
![[Pasted image 20250627120715.png]]

- **Preâmbulo e SFD:**
    - **Preâmbulo**: Usada para sincronizar os relógios do transmissor e do receptor.
    - **SFD**: Sinaliza o início real do quadro.
- **Endereço de Destino**:
    - Em uma **Requisição ARP**: Este campo é **FFFFFFFFFFFF**, que é o **end de broadcast MAC**.
    - Em uma **Resposta ARP**: Este campo é o end MAC do dispositivo que fez a Requisição ARP.
- **Endereço de Origem**: O endereço MAC do dispositivo que está enviando o quadro.
- **Tipo**: Este campo indica qual protocolo da camada superior está encapsulado nos "Dados".
- **Dados**: Esta é a área onde o **Pacote ARP** ou IP é inserido.
- **CRC**: Basicamente um checksum

---
