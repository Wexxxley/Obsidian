
---
### **1. BGP (Border Gateway Protocol):**
A  função do BGP é permitir que diferentes Sistemas Autônomos troquem informações de roteamento sobre os prefixos IP que controlam e os caminhos que podem usar para alcançar outros prefixos. Ele toma decisões de roteamento baseadas em políticas, atributos de caminho e caminhos completos.

Quando um Sistema Autônomo anuncia um prefixo via BGP, ele está dizendo: =="Olá, outros ASes! Eu sou o AS X, e eu sou o responsável por este bloco de endereços IP== (Ex, `203.0.113.0/24`). Se você tiver tráfego destinado a qualquer endereço IP dentro deste bloco você pode enviá-lo para mim, e eu sei como entregá-lo.

---
#### **1.2 Sessões BGP**
Usam o TCP para confiabilidade.
- **Sessão eBGP:** Usada para estabelecer sessões entre roteadores de borda em diferentes Sistemas Autônomos vizinhos. Através dessas sessões, os ASes trocam informações de prefixos que controlam ou que podem alcançar.
- **Sessôes iBGP**: Uma vez que um roteador de borda aprende uma rota externa, ele precisa anunciar essa rota para outros roteadores dentro do seu próprio AS para que eles saibam como rotear o tráfego para fora.
 
![[Pasted image 20250606100212.png]]
- Quando AS2 comunica um prefixo ao AS1, AS2 está prometendo que irá encaminhar todos os datagramas destinados a esse prefixo em direção ao prefixo.
- Quando um roteador aprende um novo prefixo, ele cria uma entrada para ele em sua tabela de roteamento.

---
#### **1.2 Prefixos + atributos = rota**
- **Atributo NEXT_HOP:** ==O endereço IP do próximo roteador no caminho para o prefixo de destino==. Para eBGP, é o endereço do roteador vizinho. Para iBGP, é o endereço de um roteador de borda.
- **Atributo AS_PATH:** Lista ordenada de ASes que o tráfego atravessaria para chegar ao destino. Cada vez que um prefixo é anunciado por um AS, o AS de origem adiciona seu próprio número de AS ao AS_PATH. O BGP prefere caminhos com AS_PATH mais curto.

---
#### **1.3 Processo de Seleção de Rota do BGP**
Um roteador pode aprender mais do que 1 rota para o mesmo prefixo. O roteador deve selecionar uma rota usando as regras de eleiminação.

- Atributo de valor de preferência local: decisão de política.
- AS-PATH (caminho) mais curto
- Roteador do NEXT-HOP (próximo salto) mais próximo: roteamento da “batata quente”.
- Critérios adicionais .

**1. Atributo de Valor de Preferência Local (LOCAL_PREF): Decisão de Política.**

- **O que é:** O `LOCAL_PREF` é um atributo BGP que é usado **internamente dentro de um Sistema Autônomo (AS)**. Ele não é propagado para outros ASes. É um valor numérico, e quanto **maior o valor de `LOCAL_PREF`, maior a preferência** da rota.
- **Como funciona:** Um administrador de rede pode configurar os roteadores BGP dentro de seu próprio AS para atribuir diferentes valores de `LOCAL_PREF` a rotas aprendidas de diferentes vizinhos BGP ou de diferentes fontes.
- **Decisão de Política:** Este é o **primeiro e mais poderoso critério** de seleção de rota. Ele permite que o AS implemente suas políticas de roteamento de saída. Por exemplo:
    - Um AS pode ter múltiplos provedores de Internet (ISPs). Ele pode querer que a maioria do seu tráfego de saída vá para o ISP "A" porque ele é mais barato ou tem melhor desempenho, e usar o ISP "B" apenas como backup ou para um tipo específico de tráfego. Ele faria isso configurando uma `LOCAL_PREF` mais alta para as rotas aprendidas do ISP "A".
    - Um AS geralmente configura uma `LOCAL_PREF` muito alta para rotas aprendidas de seus **clientes** (pois ele está sendo pago para transitar esse tráfego), seguida por rotas aprendidas de **pares** (peering é sem custo, então é preferível ao trânsito pago), e por último, rotas aprendidas de seus **provedores de trânsito** (que são as rotas pagas).
- **Impacto:** Se um roteador aprende duas rotas para o mesmo prefixo, uma com `LOCAL_PREF` de 200 e outra com `LOCAL_PREF` de 100, a rota com `LOCAL_PREF` de 200 será escolhida, independentemente de outros critérios.

---

**2. AS-PATH (caminho) mais curto.**

- **O que é:** O `AS_PATH` é um atributo que lista a sequência de Sistemas Autônomos que um prefixo atravessou para chegar ao AS que está anunciando a rota. Cada vez que um prefixo é anunciado de um AS para outro (via eBGP), o AS de origem adiciona seu próprio Número de Sistema Autônomo (ASN) ao início do `AS_PATH`.
- **Como funciona:** Se, após avaliar o `LOCAL_PREF`, ainda houver múltiplas rotas candidatas para o mesmo prefixo, o BGP comparará o comprimento do `AS_PATH` de cada rota.
- **Critério:** A rota com o **`AS_PATH` mais curto** é geralmente preferida. A lógica é que um caminho que passa por menos Sistemas Autônomos é, em teoria, mais direto, potencialmente mais rápido e mais confiável (menos "pontos de falha" ou intermediários).
- **Exemplo:**
    - Rota 1: `AS_PATH = (AS 701, AS 1239, AS 3356)` (3 ASes no caminho)
    - Rota 2: `AS_PATH = (AS 6453, AS 2914)` (2 ASes no caminho)
    - Neste caso, a Rota 2 seria preferida porque tem um `AS_PATH` mais curto.

---

**3. Roteador do NEXT-HOP (próximo salto) mais próximo: roteamento da “batata quente”.**

- **O que é:** O `NEXT_HOP` é o endereço IP do roteador que é o próximo salto no caminho para o prefixo de destino. Para eBGP, é o endereço IP do roteador vizinho.
- **Como funciona:** Se, após avaliar o `LOCAL_PREF` e o `AS_PATH` (e alguns outros critérios intermediários, como o `ORIGIN` e `MED` que não estão na sua lista, mas são importantes), ainda houver múltiplos caminhos de _igual_ preferência (por exemplo, dois caminhos que ambos são via peering e têm o mesmo AS_PATH), o roteador BGP precisará decidir qual gateway usar para sair do seu próprio AS.
- **Critério (da "batata quente"):** O roteador BGP consultará sua própria tabela de roteamento interna (gerada pelo protocolo intra-AS, como OSPF ou RIP) para determinar qual dos `NEXT_HOP`s possíveis está **topologicamente mais próximo** dele dentro do seu próprio AS. A rota cujo `NEXT_HOP` é alcançado com o menor custo (métrica intra-AS) será escolhida.
- **Roteamento de "Batata Quente" (Hot Potato Routing):** Este termo descreve a estratégia de encaminhar o tráfego para fora do seu próprio AS o mais rápido possível. O roteador local quer "se livrar" do pacote, enviando-o para o ponto de saída mais próximo em termos de sua própria topologia interna. Ele não se preocupa em encontrar o "melhor" caminho para o pacote _depois_ que ele sair do seu AS, apenas qual gateway de saída é o mais próximo para ele.
    - **Contraste:** O "Cold Potato Routing" seria o oposto, onde o AS tenta manter o tráfego em sua própria rede pelo maior tempo possível para garantir um caminho inter-AS mais otimizado ou preferencial para o destino final. No entanto, o "hot potato" é o comportamento padrão da maioria das implementações BGP devido à sua simplicidade e porque minimiza o uso de recursos internos do AS.

---

**4. Critérios Adicionais.**

Se, após todos os critérios acima, ainda houver empate, o BGP recorrerá a critérios adicionais, que podem variar ligeiramente entre as implementações dos fabricantes de roteadores (Cisco, Juniper, etc.), mas geralmente incluem:

- **Menor valor de MED (Multi-Exit Discriminator):** Se o AS que está anunciando a rota tiver múltiplos pontos de entrada para o seu AS, o MED pode ser usado para influenciar o AS receptor a preferir um ponto de entrada sobre outro. Um MED mais baixo é preferido. Este é um atributo que influencia o tráfego de entrada no seu AS.
- **Preferir caminhos eBGP sobre iBGP:** Se um roteador aprendeu o mesmo prefixo de um vizinho eBGP e de um vizinho iBGP, ele geralmente prefere a rota eBGP.
- **Rota mais antiga/mais estável:** Alguns roteadores preferem a rota que foi aprendida há mais tempo ou que tem sido mais estável.
- **Menor Router ID do vizinho BGP:** Se tudo mais falhar, o roteador pode escolher o caminho que leva a um vizinho BGP com o menor ID de roteador.
- **Menor endereço IP do vizinho:** Em último caso, pode ser usado o menor endereço IP do vizinho BGP como critério de desempate.



Políticas:
 Inter-AS: a administração quer ter controle sobre como seu tráfego é
roteado e sobre quem roteia através da sua rede.
 Intra-AS: administração única, então não são necessárias políticas de
decisão.
Escalabilidade
 O roteamento hierárquico poupa espaço da tabela de rotas e reduz o
tráfego de atualização.
Desempenho:
 Intra-AS: preocupação maior é desempenho.
 Inter-AS: