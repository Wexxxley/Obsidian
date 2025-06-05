
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

- Usa algoritmo do tipo Link State. Isso significa que cada roteador tem uma visão completa da **topologia da rede** em que opera.
- Usa algoritmo de Dijkstra para cálculo de rotas.
- Todas as mensagens do OSPF são autenticadas (para prevenir intrusões maliciosas).
- Múltiplos caminhos de mesmo custo são permitidos em caso de custos iguais. Ou seja, há balanceamento de carga.
- O OSPF é capaz de calcular rotas com base em diferentes **Tipos de Serviço (TOS - Type of Service)**. Isso significa que um administrador de rede pode atribuir custos diferentes a um mesmo link para diferentes tipos de tráfego.
- **Exemplo:**
    - Para tráfego "melhor esforço", como navegação web ou e-mail, um link de satélite pode ter um custo baixo, encorajando o tráfego a usá-lo mesmo com latência mais alta.
    - Para serviços de tempo real, o mesmo link de satélite pode ter um custo muito alto, desencorajando o tráfego de tempo real a usá-lo devido à alta latência.

- O OSPF tem extensões que permitem que ele não apenas roteie tráfego **unicast** (um para um), mas também forneça informações para o roteamento **multicast** (um para muitos).

##### **2.2.1 OSPF hierárquico**
- Para lidar com a escalabilidade em redes muito grandes, o OSPF introduz o conceito de **roteamento hierárquico** através de **áreas**.
    - **Backbone Area:** É a área central da rede OSPF. Todas as outras áreas precisam se conectar diretamente ou indiretamente.
    - **Áreas Regulares :** São subredes que funcionam como um OSPF completo.
    - **Roteadores de Borda de Área:** São roteadores que possuem interfaces em mais de uma área. Eles são responsáveis por resumir as informações de rota de uma área para as outras e vice-versa.
    - Roteadores de backbone: executam o roteamento OSPF de forma limitada ao
backbone.
 Roteadores de borda: conectam-se a outros ASs.
![[Pasted image 20250605190304.png]]




