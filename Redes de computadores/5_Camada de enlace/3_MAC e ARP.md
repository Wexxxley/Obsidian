
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
### Roteador Possui Tabelas ARP para Cada Rede Conectada a Ele!

Este é um ponto crucial para entender como os roteadores funcionam na Camada de Enlace:

- Um roteador não é apenas um dispositivo "de Camada 3" (IP). Ele também opera na Camada de Enlace (Camada 2) para cada interface de rede que possui.
    
- Cada porta (interface) de um roteador que está conectada a uma LAN diferente funciona como um "nó IP" independente naquela LAN.
    
- Portanto, se um roteador tem, por exemplo, três interfaces de rede (digamos, uma para a LAN da sua casa, outra para a LAN do escritório e uma para a internet), ele terá **uma tabela ARP separada para CADA UMA dessas interfaces de LAN ativas**.
    
- Cada Tabela ARP contém os mapeamentos IP-MAC para os dispositivos _naquela LAN específica_ à qual a interface está conectada.
    
- Isso permite que o roteador encaminhe pacotes de uma rede para outra: quando um pacote IP chega a uma de suas interfaces e precisa ser enviado para outra rede, o roteador primeiro consulta sua **tabela de roteamento** (na Camada 3) para decidir por qual interface o pacote deve sair. Depois de determinar a interface de saída, ele usa a **tabela ARP associada a ESSA interface de saída** para resolver o endereço MAC do próximo salto (que pode ser um host na LAN de destino ou outro roteador).
    

Em resumo, a Tabela ARP, com seu mecanismo de broadcast/unicast e o TTL, é a engrenagem essencial que permite que os dispositivos IP se localizem e se comuniquem fisicamente em redes locais, e os roteadores ampliam essa capacidade para gerenciar múltiplos segmentos de rede.


Cada nó IP numa LAN tem um módulo e uma tabela ARP.
Tabela ARP: < endereço IP; endereço MAC; TTL>

 TTL (Time To Live): tempo depois do qual o mapeamento de endereços será
esquecido (tipicamente 20 min).
 Uma solicitação ARP é sempre dada de modo broadcast e uma resposta ARP é
dada de modo unicast.

 Roteador possui tabelas ARP para cada rede conectada a ele!
1. **Verificação do Cache ARP**:
    
    - Antes de tudo, o Dispositivo A verifica sua **Tabela ARP (ou Cache ARP)**. Essa tabela é uma memória temporária onde o computador armazena mapeamentos de IP para MAC que ele aprendeu recentemente.
        
    - Se o endereço IP do Dispositivo B já estiver no cache, o Dispositivo A pega o endereço MAC correspondente e envia o quadro de dados diretamente.
        
2. **ARP Request (Requisição ARP)**:
    
    - Se o endereço IP do Dispositivo B _não_ estiver no cache, o Dispositivo A precisa "perguntar" quem possui aquele IP.
        
    - Ele então cria uma mensagem de **"ARP Request"** (Requisição ARP). Essa mensagem é um pacote de **broadcast**, o que significa que ela é enviada para _todos_ os dispositivos na rede local.
        
    - A Requisição ARP contém:
        
        - O endereço MAC do remetente (Dispositivo A).
            
        - O endereço IP do remetente (Dispositivo A).
            
        - O endereço MAC do alvo (geralmente preenchido com zeros, pois é o que se quer descobrir).
            
        - O endereço IP do alvo (Dispositivo B).
            
3. **ARP Reply (Resposta ARP)**:
    
    - Todos os dispositivos na rede local recebem a Requisição ARP. Eles verificam o "endereço IP do alvo" na Requisição.
        
    - O Dispositivo B (o único que possui aquele endereço IP) reconhece que a requisição é para ele.
        
    - O Dispositivo B, então, cria uma mensagem de **"ARP Reply"** (Resposta ARP). Essa resposta é enviada diretamente (unicast) de volta ao Dispositivo A (pois o Dispositivo B agora sabe o MAC do Dispositivo A a partir da Requisição).
        
    - A Resposta ARP contém:
        
        - O endereço MAC do remetente (Dispositivo B).
            
        - O endereço IP do remetente (Dispositivo B).
            
4. **Atualização do Cache ARP e Envio de Dados**:
    
    - O Dispositivo A recebe a Resposta ARP. Ele agora tem o mapeamento IP-MAC do Dispositivo B.
        
    - O Dispositivo A **adiciona essa nova entrada** à sua Tabela ARP para uso futuro.
        
    - Finalmente, o Dispositivo A pode encapsular o pacote IP original em um quadro de Camada de Enlace usando o endereço MAC de destino recém-descoberto e enviar os dados para o Dispositivo B.
        

### ARP em Cenários Mais Complexos:

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