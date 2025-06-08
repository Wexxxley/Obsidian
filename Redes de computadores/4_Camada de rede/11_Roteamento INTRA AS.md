

---
### **1. Protocolos de roteamento intra AS**

#### **1.1 RIP**
- Ultiliza o algoritmo de vetor de distancia
- A métrica que o RIP usa para determinar a "melhor" rota para é a **contagem de saltos**. A rota com o menor número de saltos é considerada a melhor. (MÁXIMO 15 SALTOS).
- Somente uma rota é mantida para cada destino.
- A RIP faz a troca Periódica de Tabelas de roteamento, or padrão, essa troca ocorre a cada 30 s.
- Com 180s sem retornos, o roteador considera o seu vizinho morto, descarta as rotas que passam por ele e avisa seus vizinhos.
![[Pasted image 20250605154808.png]]

**As diferenças entre RIPv1 e RIPv2:**

- **RIPv1:**
    - Não suporta prefixos de comprimento variável.
    - Não suporta autenticação.
    - Usa **broadcast** para enviar atualizações de roteamento.
- **RIPv2 (Classless):**
    - Suporta prefixos de comprimento variável.
    - Suporta autenticação.
    - Usa **multicast** para enviar atualizações de roteamento. 

---
### **2. OSPF**

- Usa algoritmo do tipo Link State. Isso significa que cada roteador tem uma visão completa da **topologia da rede** em que opera. Usa algoritmo de Dijkstra para cálculo de rotas.
- Todas as mensagens do OSPF são autenticadas (para prevenir intrusões maliciosas).
- Múltiplos caminhos de mesmo custo são permitidos em caso de custos iguais. Ou seja, há balanceamento de carga.
- O OSPF é capaz de calcular rotas com base em diferentes **Tipos de Serviço (TOS - Type of Service)**. Isso significa que um administrador de rede pode atribuir custos diferentes a um mesmo link para diferentes tipos de tráfego.
- **Exemplo:**
    - Para tráfego "melhor esforço", como navegação web ou e-mail, um link de satélite pode ter um custo baixo, encorajando o tráfego a usá-lo mesmo com latência mais alta.
    - Para serviços de tempo real, o mesmo link de satélite pode ter um custo muito alto, desencorajando o tráfego de tempo real a usá-lo devido à alta latência.

- O OSPF tem extensões que permitem que ele não apenas roteie tráfego **unicast** (um para um), mas também forneça informações para o roteamento **multicast** (um para muitos).

##### **2.1 OSPF hierárquico**
- Para lidar com a escalabilidade em redes muito grandes, o OSPF introduz o conceito de **roteamento hierárquico** através de **áreas**.
    - **Backbone Area:** É a área central da rede OSPF. Todas as outras áreas precisam se conectar diretamente ou indiretamente.
    - **Roteadores de backbone**: executam o roteamento OSPF de forma limitada ao backbone.
    - **Roteadores de borda**: conectam-se a outros ASs.
    - **Áreas Regulares :** São subredes que funcionam como um OSPF completo.
    - **Roteadores de Borda de Área:** São roteadores que possuem interfaces em mais de uma área. Eles são responsáveis por resumir as informações de rota de uma área para as outras e vice-versa.

![[Pasted image 20250605190304.png]]




