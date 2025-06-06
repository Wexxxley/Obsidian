
---
### 1. BGP (Border Gateway Protocol):
É o protocolo padrão usado entre AS.

BGP provê cada AS dos meios para:
2. Obter informações de alcance de sub-rede dos ASs Vizinhos
3. Propagar informações de alcance para todos os roteadores internos ao AS.
4. Determinar “boas” rotas para as sub-redes baseado em informações de
alcance e política.
 Permite que uma subrede comunique sua existência para o resto da Internet:
“Estou aqui”


A principal função do BGP é permitir que diferentes Sistemas Autônomos troquem informações de roteamento sobre os prefixos IP que controlam e os caminhos que podem usar para alcançar outros prefixos. Ele toma decisões de roteamento baseadas em políticas, atributos de caminho e caminhos completos.

1. **Sessões BGP (eBGP e iBGP):**
    - O BGP é usado para estabelecer sessões de adjacência entre roteadores de borda em diferentes Sistemas Autônomos. Através dessas sessões, os ASes trocam informações de prefixos que controlam ou que podem alcançar.
    - Uma vez que um roteador de borda aprende uma rota externa, ele precisa anunciar essa rota para outros roteadores dentro do seu próprio AS para que eles saibam como rotear o tráfego para fora.
2. **Prefixos e Atributos de Caminho:**
    - As mensagens BGP UPDATE carregam informações sobre os prefixos IP (redes) e um conjunto de **atributos de caminho** associados a esses prefixos. Esses atributos são cruciais para as decisões de roteamento do BGP.
    - **NEXT_HOP:** O endereço IP do próximo roteador no caminho para o prefixo de destino. Para eBGP, geralmente é o endereço IP do roteador vizinho. Para iBGP, pode ser o endereço de um roteador de borda.
    - **AS_PATH:** Talvez o atributo mais importante. É uma lista ordenada de ASes que o tráfego atravessaria para chegar ao destino. Cada vez que um prefixo é anunciado por um AS para outro via eBGP, o AS de origem adiciona seu próprio número de AS ao AS_PATH. O BGP prefere caminhos com AS_PATH mais curto (menos ASes).
    - **ORIGIN:** Indica como o prefixo foi aprendido no AS de origem (ex: IGP, EGP, Incomplete).
    - **LOCAL_PREF (Local Preference):** Um atributo que é usado _dentro_ de um AS para influenciar qual caminho de saída preferir para um destino externo quando há múltiplos caminhos disponíveis. Um valor mais alto indica maior preferência. Este atributo é trocado apenas entre pares iBGP.
    - **MED (Multi-Exit Discriminator):** Usado para influenciar _outros_ ASes sobre qual ponto de entrada preferir para o AS que o anuncia, quando há múltiplos pontos de entrada. Um valor mais baixo é preferido.
    - **COMMUNITY:** Um atributo opcional e transitório que pode ser usado para marcar rotas com informações adicionais para políticas de roteamento.
3. **Processo de Seleção de Rota do BGP:** Quando um roteador BGP recebe múltiplos anúncios para o mesmo prefixo, ele passa por um processo determinístico para escolher a "melhor" rota. A ordem exata pode variar ligeiramente entre implementações, mas geralmente segue esta sequência:
    
    1. **Preferir rota com maior LOCAL_PREF.** (Usado para tráfego de saída do AS).
    2. **Preferir rota com o AS_PATH mais curto.** (Menos ASes para atravessar).
    3. **Preferir rota com o ORIGIN code mais baixo.** (IGP < EGP < Incomplete).
    4. **Preferir rota com o MED mais baixo.** (Usado para tráfego de entrada no AS).
    5. **Preferir caminhos eBGP sobre iBGP.**
    6. **Preferir o caminho para o NEXT_HOP mais próximo (via IGP).** (Isto é onde entra o "hot potato routing").
    7. Outros critérios como BGP confederations, rota mais antiga, menor Router ID do vizinho, etc.

### Roteamento Baseado em Políticas (Policy-Based Routing)

Esta é a característica mais distintiva do BGP. Ao contrário de IGPs que geralmente usam uma única métrica para calcular o caminho mais curto, o BGP permite que as organizações implementem **políticas de roteamento complexas**. Por exemplo:

- Um AS pode decidir preferir um provedor de Internet (ISP) em relação a outro para tráfego de saída, mesmo que o caminho seja ligeiramente mais longo em termos de saltos.
- Um AS pode anunciar apenas certos prefixos para determinados vizinhos, ou filtrar prefixos recebidos para evitar tráfego indesejado.
- Um AS pode configurar regras para priorizar tráfego com base na largura de banda, custo ou acordo de nível de serviço (SLA) com um ISP.

As políticas BGP são implementadas através da manipulação dos atributos de caminho (Local_Pref, MED, Community, etc.) ou através de filtros de rota.

### Por que o BGP é Essencial para a Internet?

- **Escalabilidade:** Ele permite que a Internet cresça para bilhões de dispositivos, gerenciando as relações de roteamento entre dezenas de milhares de Sistemas Autônomos.
- **Controle e Autonomia:** Cada AS pode definir e impor suas próprias políticas de roteamento, o que é fundamental para a natureza descentralizada da Internet. Um ISP pode decidir como quer rotear o tráfego de seus clientes e como quer atrair ou desviar tráfego de outros ISPs.
- **Flexibilidade:** O BGP é extremamente flexível, permitindo diferentes topologias de interconexão entre ASes (ex: ponto a ponto, troca de tráfego em IXPs - Internet Exchange Points).
- **Resiliência:** Embora as mudanças na topologia possam levar algum tempo para convergir (especialmente em comparação com IGPs), o BGP é projetado para lidar com falhas e mudanças na rede, encontrando caminhos alternativos.

### Limitações e Desafios

- **Complexidade:** O BGP é notoriamente difícil de configurar e depurar. Erros de configuração podem ter um impacto significativo e generalizado na Internet (ex: sequestro de rotas).
- **Convergência:** A convergência do BGP pode ser mais lenta do que a dos IGPs devido ao volume de informações, à natureza orientada a políticas e ao uso de TCP.
- **Segurança:** Historicamente, o BGP não incluía mecanismos de segurança robustos, tornando-o vulnerável a ataques como sequestro de rotas (route hijacking), onde um AS mal-intencionado anuncia prefixos IP que não possui, desviando o tráfego. Esforços como o RPKI (Resource Public Key Infrastructure) estão sendo feitos para melhorar a segurança do roteamento BGP.

Em resumo, o BGP é a espinha dorsal do roteamento da Internet, permitindo a interconexão de redes administradas de forma independente. Sua força reside em sua capacidade de roteamento baseado em políticas e em sua escalabilidade, o que o torna indispensável para o funcionamento da rede global.