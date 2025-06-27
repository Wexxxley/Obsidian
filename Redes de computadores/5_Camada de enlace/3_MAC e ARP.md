
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
        
- **Endereço Físico de Origem (Por exemplo, 6 bytes para Ethernet)**: O endereço MAC do dispositivo que está enviando o pacote ARP (seja uma solicitação ou resposta).
    
- **Protocolo do Endereço de Origem (Por exemplo, 4 bytes para IP)**: O endereço IP do dispositivo que está enviando o pacote ARP.
    
- **Endereço Físico de Destino (Por exemplo, 6 bytes para Ethernet) (Não é preenchido numa solicitação)**:
    
    - Em uma **Requisição ARP**: Este campo é geralmente preenchido com zeros (ou qualquer valor que não seja um MAC válido), pois é o endereço MAC que o solicitante quer descobrir.
        
    - Em uma **Resposta ARP**: Este campo é preenchido com o endereço MAC do dispositivo que fez a solicitação original.
        
- **Protocolo do Endereço de Destino (Por exemplo, 4 bytes para IP)**: O endereço IP do dispositivo para o qual a solicitação é feita (na Requisição ARP) ou para o qual a resposta é destinada (na Resposta ARP).
    

---

### 2. Pacote de Solicitação e Resposta ARP (Encapsulado em um Quadro Ethernet)

A parte inferior da imagem mostra como o **Pacote ARP** (os "Dados" na imagem) é encapsulado dentro de um **Quadro Ethernet** para ser transmitido fisicamente pela rede.

- **Preâmbulo e SFD (Start Frame Delimiter) - 8 bytes**:
    
    - **Preâmbulo**: Uma sequência de bits alternados (10101010...) usada para sincronizar os relógios do transmissor e do receptor.
        
    - **SFD**: Uma sequência específica de 1 byte (10101011) que sinaliza o início real do quadro Ethernet.
        
    - _Estes são campos da Camada Física e geralmente não são vistos em capturas de pacotes da Camada de Enlace, pois são removidos pelo hardware antes de passar os dados para o driver._
        
- **Endereço de Destino (6 bytes)**:
    
    - Em uma **Requisição ARP**: Este campo é **FFFFFFFFFFFF** (todos os bits em 1), que é o **endereço de broadcast MAC**. Isso garante que _todos_ os dispositivos na rede local recebam e processem a Requisição ARP.
        
    - Em uma **Resposta ARP**: Este campo é o endereço MAC do dispositivo que originalmente fez a Requisição ARP (tornando a resposta um pacote **unicast**).
        
- **Endereço de Origem (6 bytes)**: O endereço MAC do dispositivo que está enviando o quadro Ethernet (e, portanto, o pacote ARP encapsulado).
    
- **Tipo (2 bytes)**: Este campo indica qual protocolo da camada superior está encapsulado nos "Dados" do quadro Ethernet.
    
    - Para um Pacote ARP, o valor é **`0x0806`** (hexadecimal). Este valor é o identificador oficial para o protocolo ARP. Quando uma NIC recebe um quadro com `Tipo = 0x0806`, ela sabe que o payload contém um pacote ARP e o entrega ao módulo ARP para processamento.
        
    - (Para um pacote IP, por exemplo, o tipo seria `0x0800`).
        
- **Dados**: Esta é a área onde o **Pacote ARP** (cuja estrutura foi detalhada na parte superior da imagem) é inserido.
    
- **CRC (Cyclic Redundancy Check) - 4 bytes**: Uma sequência de bits calculada a partir de todos os campos anteriores do quadro. O receptor recalcula o CRC e o compara com o valor recebido. Se forem diferentes, indica que houve um erro na transmissão do quadro.
    

---

### Endereço de Destino em uma Solicitação é FFFFFFFFFFFF.

Esta frase no canto superior direito reforça um ponto crucial:

- Em uma **Requisição ARP**, o objetivo é descobrir o endereço MAC de um dispositivo cujo IP você conhece, mas cujo MAC você _não_ conhece.
    
- Como você não sabe para quem enviar a pergunta, a Requisição ARP é enviada para o **endereço MAC de broadcast (`FF:FF:FF:FF:FF:FF`)**. Isso assegura que todos os dispositivos na rede local recebam a Requisição e possam verificar se o IP perguntado pertence a eles.
    

Em suma, esta imagem ilustra perfeitamente como o protocolo ARP preenche a lacuna entre os endereços IP (lógicos, de rede) e os endereços MAC (físicos, de enlace), permitindo que os dispositivos se encontrem e se comuniquem dentro de uma mesma rede local através do encapsulamento em quadros Ethernet.



- **Comunicação com dispositivos fora da rede local**: Se o Dispositivo A quer enviar dados para um Dispositivo C que está em outra rede, ele não usará o ARP para descobrir o MAC do Dispositivo C. Em vez disso, ele usará o ARP para descobrir o endereço MAC do seu **Gateway Padrão** (o roteador que conecta sua rede local à internet ou a outras redes). O roteador, então, assume a responsabilidade de encaminhar o pacote para o destino final.
    
- **Proxy ARP**: Um roteador pode responder a Requisições ARP em nome de um dispositivo em outra sub-rede para o qual ele pode rotear o tráfego. Isso faz com que os dispositivos pareçam estar na mesma rede local, mesmo não estando.
    
- **ARP Gratuito (Gratuitous ARP)**: Um dispositivo pode enviar uma Resposta ARP não solicitada (sem ter recebido uma Requisição) para anunciar seu próprio endereço IP e MAC para a rede. Isso é útil para:
    
    - Detectar conflitos de IP (se outro dispositivo responder com o mesmo IP).
        
    - Atualizar o cache ARP dos outros dispositivos após uma mudança de endereço IP ou um failover.
        

### Importância e Implicações de Segurança:

O ARP é vital para a comunicação em redes locais. Sem ele, os administradores teriam que configurar manualmente tabelas de mapeamento IP-MAC em cada dispositivo, o que seria impraticável.

No entanto, o ARP é um protocolo que opera "na base da confiança". Uma Requisição ARP espera uma Resposta ARP válida, mas não há autenticação. Isso o torna vulnerável a ataques como:

- **ARP Spoofing (Envenenamento de Cache ARP)**: Um atacante envia respostas ARP falsas para enganar os dispositivos da rede, fazendo-os associar o IP de outro dispositivo (ou do gateway) ao MAC do atacante. Isso pode levar a ataques "Man-in-the-Middle" (o atacante intercepta todo o tráfego), negação de serviço, etc.
    

Em resumo, o ARP é o "agente de busca" da rede local, que permite que os dispositivos encontrem uns aos outros fisicamente com base em seus endereços lógicos, facilitando a comunicação diária que consideramos tão natural.