
---

### **1. Endereço MAC/LAN/FÍSICO**
- Usado para levar o datagrama de uma interface física a outra na mesma rede.
- Endereços MAC tem 48 bits. Cada placa de rede no mundo possui seu end físico
- É gravado na memória fixa ROM do adaptador de rede.
- A alocação de endereços MAC é administrada pelo IEEE.
- O fabricante compra porções do espaço de endereço MAC. 
- Endereçamento MAC possui portabilidade, ou seja, sua máquina pode ter o mesmo end MAC mesmo em redes diferentes. Para isso, não pode ter duas máquinas com o mesmo end físico.
- Se for preciso mudar o end MAC, os drivers omitem o end da ROM e usam outro.

---
### **2. ARP (Address Resolution Protocol)** 

Ele descobre o endereço MAC de um dispositivo a partir do endereço IP.

Imagine que seu computador (Dispositivo A) quer enviar um pacote de dados para outro computador (Dispositivo B) na mesma rede local. O Dispositivo A sabe o **endereço IP** do Dispositivo B. No entanto, para que o pacote seja entregue fisicamente pela rede, o Dispositivo A precisa saber o **endereço MAC** do Dispositivo B.


Cada Nó IP (Host, Roteador) Numa LAN Tem um Módulo e Uma Tabela ARP
- **Módulo ARP**: Componente de software responsável por executar as operações do protocolo ARP.
- **Tabela ARP**: Associada a esse módulo, cada nó mantém uma **Tabela ARP**. É uma lista de mapeamentos entre endereços IP e seus correspondentes endereços MAC para dispositivos que o nó descobriu recentemente na mesma rede local.
	![[Pasted image 20250627115140.png]]
	- **`Time To Live)`**: O **Tempo de Vida** para aquela entrada na tabela, tipicamente 20 min.

- **Solicitação ARP (ARP Request) - Broadcast**: Quando um dispositivo precisa descobrir um endereço MAC para um IP que não está em sua tabela, ele pergunta para _todos_ na rede local. 
- **Resposta ARP (ARP Reply) - Unicast**: O dispositivo que possui o endereço IP alvo recebe a Requisição ARP. Como ele agora sabe o endereço MAC do remetente da requisição, ele pode enviar a **Resposta ARP** diretamente de volta para o solicitante. 

- Cada porta (interface) de um roteador que está conectada a uma LAN diferente funciona como um "nó IP" independente. Portanto, se um roteador tem, por exemplo, três interfaces de rede, ele terá **uma tabela ARP separada para CADA UMA dessas interfaces de LAN ativas**.

**Funcionamento na mesma rede**
![[Pasted image 20250627115648.png]]

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
	- O pacote ARP e o IP possuem diferentes sinalizações.
- **Dados**: Esta é a área onde o **Pacote ARP** ou IP é inserido.
- **CRC**: Uma sequência de bits calculada a partir de todos os campos anteriores do quadro. O receptor recalcula o CRC e o compara com o valor recebido. 

---
### **4. ARP casos complexos**

Máquina A (na Rede 1) Quer Falar com Máquina B (na Rede 2)

1. **A cria o pacote IP com origem A, destino B.**
    - **Ponto Chave**: A máquina A, ao verificar o endereço IP de destino (B), percebe que B _não está na mesma rede local_. Como ela sabe disso? Comparando o endereço IP de destino com sua própria máscara de sub-rede e o endereço IP do gateway padrão configurado.
    - Como B está em outra rede, A não tenta descobrir o MAC de B diretamente. Em vez disso, A precisa enviar o pacote para seu **gateway padrão** (o roteador R).
    - Então, A executa um processo ARP: ele envia uma Requisição ARP perguntando: "Quem tem o IP `111.111.111.110`?".
    - O roteador R (o gateway padrão de A) responde com seu endereço MAC para aquela interface.
2. **A cria um quadro Ethernet com o endereço físico de R como destino, o quadro Ethernet contém o datagrama IP de A para B.**
    
    - Agora que A tem o endereço MAC do roteador R, ele pode construir o **quadro Ethernet** (Camada de Enlace).
        
    - O **endereço MAC de destino** do quadro Ethernet será o MAC do **roteador R** (o próximo salto).
        
    - O **endereço MAC de origem** será o MAC da máquina A.
        
    - Dentro da parte de "Dados" (payload) deste quadro Ethernet está o **datagrama IP original**, que tem o endereço IP de origem A e o endereço IP de destino B.
        
    - A máquina A envia este quadro para o roteador R.
        
3. **A camada de enlace de R recebe o quadro Ethernet enviado por A.**
    
    - A interface do roteador R que está conectada à Rede de A recebe o quadro Ethernet.
        
    - O roteador verifica o endereço MAC de destino do quadro. Como é o seu próprio endereço MAC, ele aceita o quadro.
        
4. **R remove o datagrama IP do quadro Ethernet, verifica que ele se destina a B.**
    
    - O roteador R desencapsula o quadro Ethernet, removendo os cabeçalhos da Camada de Enlace.
        
    - Ele agora tem o **datagrama IP original**.
        
    - O roteador examina o **endereço IP de destino (B)** no datagrama IP. Ele consulta sua **tabela de roteamento** (na Camada de Rede) para determinar a melhor rota para o endereço IP de B. A tabela de roteamento dirá a R por qual de suas interfaces o pacote deve sair para chegar à rede de B.
        
5. **R usa ARP para obter o endereço físico de B.**
    
    - **Ponto Crítico**: O roteador R agora sabe que o pacote precisa ir para a Rede 2 e que o destino final é B. Se B for um dispositivo diretamente conectado àquela outra interface do roteador (na Rede 2), o roteador precisará do endereço MAC de B.
        
    - Então, R inicia um novo processo ARP, **nesta outra rede (Rede 2)**. Ele envia uma Requisição ARP na Rede 2 perguntando: "Quem tem o IP de B?".
        
    - A máquina B responde com seu endereço MAC.
        
6. **R cria quadro contendo um datagrama de A para B e envia para B.**
    
    - Com o endereço MAC de B em mãos, o roteador R agora cria um **novo quadro Ethernet** (ou o tipo de quadro apropriado para a Rede 2, se não for Ethernet).
        
    - O **endereço MAC de destino** deste _novo_ quadro será o MAC da máquina **B**.
        
    - O **endereço MAC de origem** será o MAC da interface do próprio roteador R que está conectada à Rede 2.
        
    - Dentro desse novo quadro ainda estará o **datagrama IP original (de A para B)**.
        
    - O roteador R envia este quadro diretamente para a máquina B.
