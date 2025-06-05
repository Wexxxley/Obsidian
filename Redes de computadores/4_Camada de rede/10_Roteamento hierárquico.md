
---

### **1. Roteamento hierárquico**
Cada administração de rede pode querer controlar o roteamento na sua
própria rede. Ai que surgem os  “sistemas autônomos ” (AS).

- **Roteamento Intra-AS:** Dentro de cada AS, os roteadores executam o mesmo protocolo de roteamento. Esses protocolos são responsáveis por estabelecer entradas de roteamento para destinos localizados _dentro_ do mesmo AS.
- **Roteamento Inter-AS:** Refere-se aos protocolos de roteamento usados para trocar informações de roteamento _entre_ diferentes AS. 
- **Roteadores Gateway:** São roteadores que possuem links diretos para roteadores em outros AS. 

![[Pasted image 20250605152214.png]]

Quando um roteador no AS1 recebe um datagrama cujo destino está fora do AS1, ele não possui, por si só, essa informação. É aqui que entram os protocolos de roteamento inter-AS e intra-AS.

**1. Aprender quais destinos são alcançáveis através de AS2 e através de AS3.**
- **Tarefa para o roteamento inter-AS!** Os roteadores de _gateway_ do AS1 estabelecem sessões BGP (Border Gateway Protocol) com os roteadores de _gateway_ dos ASs vizinhos. Através dessas sessões, o AS1 aprende sobre as sub-redes que são anunciadas por AS2 e AS3. 

**2. Propagar suas informações de alcance para todos os roteadores em AS1.**
- Uma vez que os roteadores de _gateway_ do AS1 aprendem sobre os destinos externos, essa informação precisa ser distribuída para os demais roteadores dentro do AS1. **Isso é feito pelo protocolo intra-AS.** 

**Cenário: AS1 aprende que a sub-rede 'x' é alcançável através de AS3 e através de AS2.**
- **Roteamento de “batata-quente”
    - A ideia da "batata-quente" é que o AS local quer se livrar do pacote o mais rápido possível, encaminhando-o para o ponto de saída mais próximo em termos de métrica interna 

---
### **2. Protocolos de roteamento intra AS**

#### **2.1 RIP**
- Ultiliza o algoritmo de vetor de distancia
- A métrica que o RIP usa para determinar a "melhor" rota para é a **contagem de saltos**. A rota com o menor número de saltos é considerada a melhor. (MÁXIMO 15 SALTOS).
- Somente uma rota é mantida para cada destino.
- A RIP faz a troca Periódica de Tabelas de roteamento, or padrão, essa troca ocorre a cada 30 s.
- Com 180s sem retornos, o roteador considera o seu vizinho morto, descarta as rotas que passam por ele e avisa seus vizinhos.
![[Pasted image 20250605154808.png]]
- RIP V1: Sem criptografia,
- RIP V2: Tem criptografia, 

---
### **2.2 OSPF**

**- Usa algoritmo do tipo Link State.**

- **Detalhe:** Ao contrário do RIP (que é vetor de distância e "roteia por boato"), o OSPF é um protocolo de roteamento do tipo **estado de enlace**. Isso significa que cada roteador OSPF não apenas sabe quais são seus vizinhos e a distância até eles, mas também tem uma visão completa da **topologia da rede** em que opera.
- **Como funciona:** Cada roteador OSPF gera um **Link State Advertisement (LSA)**, que é uma pequena "propaganda" que descreve seus links diretos, seus estados (ativo/inativo), a custo associado a cada link e os vizinhos aos quais está conectado. Esses LSAs são a base para construir o "mapa" da rede.

**- Mapa topológico em cada nó.**

- **Detalhe:** Cada roteador OSPF recebe os LSAs de _todos_ os outros roteadores na sua área (ou no AS, se não houver áreas). Ele usa esses LSAs para construir e manter uma **Base de Dados de Estado de Enlace (LSDB - Link State Database)**. A LSDB é, essencialmente, um **mapa completo e idêntico da topologia da rede** em todos os roteadores OSPF dentro de uma mesma área.
- **Benefício:** Ter um mapa completo permite que cada roteador calcule as rotas de forma independente e mais precisa, evitando os problemas de "roteamento por boato" e os loops de roteamento comuns em protocolos de vetor de distância.

**- Usa algoritmo de Dijkstra para cálculo de rotas.**

- **Detalhe:** Uma vez que cada roteador tem o mapa completo da rede (sua LSDB), ele aplica o **Algoritmo de Dijkstra (também conhecido como Algoritmo SPF - Shortest Path First)**. Este algoritmo calcula a árvore de caminhos mais curtos a partir do próprio roteador para _todos_ os outros destinos na rede. O roteador age como a raiz dessa árvore.
- **Benefício:** O resultado do algoritmo de Dijkstra é a **tabela de roteamento**, que contém os melhores caminhos para todos os destinos conhecidos, baseados na métrica de custo OSPF.

**- Anúncios do OSPF transportam um registro para cada roteador vizinho.**

- **Detalhe:** Os LSAs (Link State Advertisements) que os roteadores OSPF geram e trocam contêm informações detalhadas sobre os links de um roteador e seus vizinhos. Por exemplo, um LSA de roteador pode incluir:
    - O Router ID do roteador que o originou.
    - A lista de interfaces ativas do roteador.
    - Para cada interface, o ID do roteador vizinho conectado a essa interface.
    - O custo (métrica) associado a cada link.
    - Informações sobre sub-redes conectadas diretamente.
- **Propósito:** Esses registros são cruciais para que todos os roteadores possam construir o mapa preciso da topologia.

**- Anúncios são distribuídos para todo o AS (via flooding).**

- **Detalhe:** Quando um roteador OSPF gera um LSA (seja por uma mudança na topologia ou periodicamente), ele o envia para todos os seus vizinhos. Cada vizinho, por sua vez, armazena o LSA em sua LSDB (se for uma informação nova ou mais recente) e o retransmite para _todos_ os seus outros vizinhos, exceto a interface pela qual o LSA foi recebido. Esse processo é chamado de **flooding (inundação)**.
- **Controle do flooding:** Para evitar loops de flooding e garantir que os LSAs sejam distribuídos eficientemente, o OSPF usa sequências de números (sequence numbers) e temporizadores de "vida" (LSA age) para garantir que apenas os LSAs mais recentes e válidos sejam mantidos e propagados.

**- Todas as mensagens do OSPF são autenticadas (para prevenir intrusões maliciosas).**

- **Detalhe:** OSPF suporta diferentes tipos de autenticação para garantir que apenas roteadores confiáveis e autorizados possam participar do processo de roteamento. Isso impede que roteadores mal-intencionados injetem informações de roteamento falsas, que poderiam levar a ataques de negação de serviço, desvios de tráfego ou outros problemas de segurança.
- **Tipos de Autenticação:**
    - **Autenticação Simples por Senha (Plain Text):** A senha é enviada em texto puro, o que é inseguro.
    - **Autenticação MD5:** Usa um hash criptográfico (MD5) da senha para verificar a integridade da mensagem, oferecendo um nível de segurança muito maior.
    - **Autenticação HMAC-SHA:** Métodos mais recentes e mais fortes de hashing criptográfico.

**- Múltiplos caminhos de mesmo custo são permitidos em caso de custos iguais. Ou seja, há balanceamento de carga.**

- **Detalhe:** Se o algoritmo de Dijkstra encontrar dois ou mais caminhos para o mesmo destino que tenham exatamente o mesmo custo total (soma dos custos dos links), o OSPF pode usar todos esses caminhos em paralelo.
- **Benefício:** Isso é conhecido como **ECMP (Equal-Cost Multi-Path)**. O roteador pode distribuir o tráfego entre esses caminhos, o que resulta em **balanceamento de carga**, aumentando a utilização da largura de banda disponível e melhorando a resiliência da rede.

**- Para cada link, múltiplas métricas de custo para TOS diferentes (ex., custo de enlace por satélite definido baixo para tráfego de “melhor esforço” e alto para serviços de tempo real).**

- **Detalhe:** O OSPF é capaz de calcular rotas com base em diferentes **Tipos de Serviço (TOS - Type of Service)**. Isso significa que um administrador de rede pode atribuir custos diferentes a um mesmo link para diferentes tipos de tráfego.
- **Exemplo:**
    - Para tráfego "melhor esforço" (best-effort), como navegação web ou e-mail, um link de satélite pode ter um custo baixo, encorajando o tráfego a usá-lo mesmo com latência mais alta.
    - Para serviços de tempo real, como voz ou vídeo, o mesmo link de satélite pode ter um custo muito alto, desencorajando o tráfego de tempo real a usá-lo devido à alta latência.
- **Benefício:** Essa capacidade permite o **roteamento baseado em política** e o **gerenciamento de qualidade de serviço (QoS)**, onde o tráfego pode ser direcionado por caminhos que são mais adequados para suas características específicas (ex., menor atraso para voz, maior largura de banda para transferência de arquivos grandes).

**- Integra tráfego uni- e multicast:**

- **Detalhe:** O OSPF tem extensões que permitem que ele não apenas roteie tráfego **unicast** (um para um), mas também forneça informações para o roteamento **multicast** (um para muitos).
- **MOSPF (Multicast OSPF):** Uma extensão que permite a descoberta de grupos multicast e a construção de árvores de distribuição multicast dentro do domínio OSPF.
- **Benefício:** Simplifica a implantação de aplicações multicast em redes OSPF, como videoconferências e transmissão de mídia.

**- OSPF hierárquico: OSPF para grandes domínios.**

- **Detalhe:** Para lidar com a escalabilidade em redes muito grandes, o OSPF introduz o conceito de **roteamento hierárquico** através de **áreas**.
- **Como funciona:**
    - **Área 0 (Area 0 ou Backbone Area):** É a área central da rede OSPF. Todas as outras áreas precisam se conectar diretamente ou indiretamente à Área 0.
    - **Áreas Regulares (Non-Backbone Areas):** São subseções da rede. Os roteadores dentro de uma área mantêm apenas a LSDB da sua própria área, não da rede OSPF inteira.
    - **Roteadores de Borda de Área (ABRs - Area Border Routers):** São roteadores que possuem interfaces em mais de uma área (incluindo a Área 0). Eles são responsáveis por resumir as informações de rota de uma área para as outras e vice-versa, reduzindo o volume de LSAs que precisam ser trocados entre áreas.
- **Benefícios:**
    - **Redução da LSDB:** Cada roteador mantém um mapa topológico menor, reduzindo o uso de memória.
    - **Redução do processamento do Dijkstra:** O algoritmo SPF é executado apenas para a própria área, resultando em menor carga de CPU.
    - **Redução do flooding:** O flooding de LSAs é contido dentro de cada área.
    - **Convergência mais rápida:** Uma mudança em uma área afeta principalmente os roteadores dentro dessa área, minimizando o impacto em outras áreas.

Em resumo, o OSPF é um protocolo de roteamento robusto, escalável e rico em recursos, adequado para redes de tamanho médio a grande, graças à sua abordagem de estado de enlace, cálculo de rotas via Dijkstra, suporte a balanceamento de carga, QoS e arquitetura hierárquica por áreas.






