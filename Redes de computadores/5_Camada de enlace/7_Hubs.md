
---

Um hub opera na **Camada 1 (Física)**. Um hub é basicamente um repetidor de sinais elétricos. Ele não "entende" os dados da mesma forma que um switch ou roteador.

- **Broadcast**: Quando um bit chega a uma das portas do hub, ele é imediatamente copiado e enviado para _todas_ as outras portas conectadas. Isso significa que todos os dispositivos conectados ao hub recebem cada bit de dados transmitido por qualquer outro dispositivo no mesmo hub.
- **Um hub não faz conversão de velocidade**.
- **Não possuem armazenagem de quadros.** Ao contrário de um switch, um hub não tem memória para armazenar quadros de dados.
- É importante entender que o mecanismo CSMA/CD não é implementado _dentro_ do hub. Em vez disso, a detecção e o tratamento de colisões ocorrem nos **adaptadores de rede** de cada dispositivo final conectado ao hub. 
- **Domínio de colisão**: Um "domínio de colisão" é uma área da rede onde as colisões de dados podem ocorrer. Como um hub simplesmente retransmite tudo para todos, todos os dispositivos conectados a um hub fazem parte de um **único e grande domínio de colisão**.
![[Pasted image 20250702154313.png]]


---
### **Switch**
Um switch é um **dispositivo de camada de enlace**. Diferente dos hubs, os switches são capazes de "entender" e processar os quadros Ethernet.

- **Armazena e encaminha quadros Ethernet:** Ao receber um quadro de dados, o switch o armazena temporariamente antes de tomar uma decisão de encaminhamento.
- **Unicast**: Um switch lê o **endereço MAC** de destino e encaminha o quadro apenas para a porta específica. Isso cria "micro-segmentos", onde cada porta se torna um domínio de colisão individual.

**2. Transparência e Facilidade de Uso:**

- **Transparente:** A operação de um switch é transparente para os dispositivos finais (hospedeiros ou "hosts"). Isso significa que os computadores conectados à rede não "percebem" a presença do switch; eles simplesmente enviam seus dados, e o switch cuida do encaminhamento inteligente. Não há necessidade de configurar os dispositivos finais para funcionar com o switch.
    
- **Plug-and-play e auto-aprendizado:** A maioria dos switches (especialmente os não gerenciáveis) são "plug-and-play". Isso significa que eles funcionam automaticamente assim que são conectados, sem a necessidade de configuração manual. Essa capacidade é possível devido ao seu recurso de "auto-aprendizado".
    

**3. Como um Switch "Aprende" e a Tabela de Switch (MAC Address Table):**

A inteligência de um switch reside em sua capacidade de aprender as localizações dos dispositivos conectados a ele. Para isso, ele mantém uma **tabela de switch**, também conhecida como Tabela MAC ou Tabela CAM (Content Addressable Memory).

- **Estrutura da Entrada na Tabela:** Cada entrada na tabela de switch contém tipicamente:
    
    - **Endereço MAC:** O endereço físico exclusivo de um dispositivo de rede.
        
    - **Interface:** A porta física do switch à qual o dispositivo com aquele endereço MAC está conectado.
        
    - **Marca de Tempo (Timestamp):** Um registro de quando a entrada foi aprendida ou a última vez que o dispositivo foi visto.
        
- **Como o Aprendizado Acontece:** Quando um switch recebe um quadro de dados em uma de suas interfaces, ele automaticamente **"aprende" a localização do transmissor**.
    
    - Ele lê o **endereço MAC de origem** do quadro que acabou de receber.
        
    - Ele associa esse endereço MAC de origem à interface (porta) pela qual o quadro chegou.
        
    - Ele registra essa associação (par transmissor/localização) na sua tabela de switch, junto com uma marca de tempo. Assim, o switch sabe qual host pode ser alcançado através de suas interfaces.
        
- **Manutenção da Tabela:**
    
    - As **entradas expiradas na tabela são descartadas**. Cada entrada tem um tempo de vida (TTL - Time To Live), que pode ser, por exemplo, 60 minutos. Se um dispositivo não transmitir por esse período, sua entrada é removida, mantendo a tabela atualizada e eficiente.
        

**4. Como um Switch Encaminha um Quadro (Lógica de Encaminhamento):**

Quando um switch recebe um quadro Ethernet, ele segue uma lógica precisa para decidir como encaminhá-lo:

1. **Indexa a Tabela:** O switch primeiro verifica o **endereço MAC de destino** no cabeçalho do quadro. Ele usa esse endereço para pesquisar em sua tabela de switch.
    
2. **Se a Entrada for Encontrada para o Destino:**
    
    - **Se o endereço MAC de destino for encontrado na tabela**, o switch sabe exatamente em qual interface o dispositivo de destino está conectado.
        
    - **Transmite o quadro:** O switch então encaminha o quadro _somente_ para essa interface específica.
        
    - **Descarte se na mesma interface:** Há uma condição especial: se o quadro chegou em uma interface e o endereço MAC de destino também está associado à _mesma_ interface na tabela, o switch simplesmente **descarta o quadro**. Isso ocorre porque o quadro já alcançou o segmento de rede onde o destino reside, e não há necessidade de retransmiti-lo (um cenário comum em redes com múltiplos switches ou em certas configurações).
        
    - **Reencaminha se em outra interface:** Caso contrário (se o destino está em uma interface diferente da de origem), ele reencaminha o quadro na interface indicada na tabela.
        
3. **Se Nenhuma Entrada for Encontrada para o Destino (Flood):**
    
    - **Inundação (Flood):** Se o switch **não encontrar o endereço MAC de destino** em sua tabela (porque é um dispositivo novo na rede ou a entrada expirou), ele não sabe onde enviar o quadro seletivamente. Nesse caso, ele entra em modo de **inundação (flood)**.
        
    - Isso significa que o switch **encaminha o quadro para todas as suas interfaces, exceto para a interface pela qual o quadro chegou**. Isso garante que o quadro alcance seu destino (que provavelmente responderá, permitindo que o switch aprenda sua localização para futuras comunicações) e é uma forma de "descoberta" de endereços MAC.
        

Em resumo, os switches revolucionaram as redes locais ao trazer inteligência para a Camada 2, eliminando a ineficiência dos hubs através do encaminhamento seletivo baseado em endereços MAC e da criação de múltiplos domínios de colisão, resultando em redes mais rápidas, eficientes e confiáveis.