
---

Um hub opera na **Camada 1 (Física)**. Um hub é basicamente um repetidor de sinais elétricos. Ele não "entende" os dados da mesma forma que um switch ou roteador.

- Quando um bit chega a uma das portas do hub, ele é imediatamente copiado e enviado para _todas_ as outras portas conectadas. Isso significa que todos os dispositivos conectados ao hub recebem cada bit de dados transmitido por qualquer outro dispositivo no mesmo hub.
- **"Com a mesma taxa."**
    
    - Um hub não faz conversão de velocidade. Se uma porta está configurada para 10 Mbps, todas as outras portas operarão a 10 Mbps (ou se for um hub de 10/100 Mbps, todas as portas operariam na mesma velocidade definida ou negociada, mas sem segmentação de velocidade por porta).
        
- **"Não possuem armazenagem de quadros."**
    
    - Ao contrário de um switch, um hub não tem memória para armazenar quadros de dados. Ele não faz buffering. Os dados são simplesmente repetidos em tempo real, bit por bit. Essa falta de inteligência é uma das razões para suas limitações de desempenho.
        
- **"Não há CSMA/CD no hub: adaptadores detectam colisões."**
    
    - É importante entender que o mecanismo CSMA/CD (Carrier Sense Multiple Access with Collision Detection) não é implementado _dentro_ do hub. Em vez disso, a detecção e o tratamento de colisões ocorrem nos **adaptadores de rede (placas de rede)** de cada dispositivo final conectado ao hub. Como o hub propaga todos os bits para todas as portas, se dois dispositivos transmitirem ao mesmo tempo, os sinais colidem no meio físico compartilhado, e os adaptadores de rede de cada dispositivo são responsáveis por detectar essa colisão e iniciar o processo de _backoff_ exponencial para retransmitir, conforme explicado anteriormente.
        
- **"Provê funcionalidade de gerenciamento de rede."**
    
    - Embora a funcionalidade principal dos hubs seja simples repetição, alguns hubs mais sofisticados (chamados "hubs gerenciáveis") poderiam oferecer recursos básicos de gerenciamento, como ligar/desligar portas, monitorar o tráfego geral ou estatísticas simples. No entanto, esses recursos são muito limitados em comparação com os de um switch gerenciável.
        
- **"Domínios de colisão individuais tornam-se um único e grande domínio de colisão. (Obsoleto!)"**
    
    - Este é o ponto mais crítico e a principal razão pela qual os hubs são considerados **obsoletos** em redes modernas. Um "domínio de colisão" é uma área da rede onde as colisões de dados podem ocorrer. Como um hub simplesmente retransmite tudo para todos, todos os dispositivos conectados a um hub (e a outros hubs conectados a ele, como no diagrama) fazem parte de um **único e grande domínio de colisão**.
        
    - Isso significa que, à medida que mais dispositivos são adicionados e o tráfego aumenta, a probabilidade de colisões também aumenta exponencialmente. As colisões reduzem drasticamente o desempenho da rede, pois os dados precisam ser retransmitidos, consumindo largura de banda e tempo. Para redes modernas que exigem alta performance e confiabilidade, essa limitação é inaceitável.
        

**Diagrama de Hierarquia de Hubs:**

A imagem ilustra uma topologia hierárquica usando hubs:

- **Hub de Backbone:** No topo, há um hub central ("Hub de backbone") que conecta outros hubs.
    
- **Hub 10BaseT:** Abaixo do hub de backbone, há três hubs 10BaseT menores. Cada um desses hubs conecta um grupo de estações de trabalho (computadores).
    
- **Segmentação:** O diagrama mostra grupos de computadores para "Engenharia elétrica", "Ciência da computação" e "Engenharia de sistemas". Embora os hubs criem essa segmentação lógica em grupos de trabalho, é fundamental entender que, fisicamente, toda essa estrutura ainda representa um **único e grande domínio de colisão**. Qualquer transmissão de um computador na "Engenharia elétrica" seria propagada para todos os outros computadores nos outros hubs e segmentos através do hub de backbone.
    

**Conclusão (Obsoleto!):**

Devido à sua natureza de criação de um único e grande domínio de colisão, que limita severamente o desempenho da rede em cenários de múltiplos usuários, os hubs foram amplamente substituídos por **switches**. Switches são dispositivos mais inteligentes que operam na Camada 2 (Enlace de Dados), criam micro-segmentos (domínios de colisão individuais por porta) e aprendem as localizações dos dispositivos, encaminhando o tráfego apenas para a porta de destino correta, o que aumenta drasticamente a eficiência e o desempenho da rede.