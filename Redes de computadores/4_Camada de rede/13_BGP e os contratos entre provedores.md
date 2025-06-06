

---

### 1. Contratos de Trânsito 

- **O que é:** Um contrato de trânsito ocorre quando uma rede (geralmente menor ou "downstream") paga a outra rede (geralmente maior ou "upstream") para ter acesso à _Internet completa_. Em outras palavras, o provedor de trânsito concorda em levar o tráfego da rede downstream para _qualquer_ destino na Internet, e também a entregar o tráfego de _qualquer_ lugar da Internet para a rede downstream.
    
- **Analogia:** É como se você pagasse a um provedor de internet (seu ISP) para ter acesso a todos os sites e serviços online. Seu ISP é seu provedor de trânsito para a Internet.
    
- **Impacto no BGP:**
    
    - **Anúncios de Prefixo:** O provedor de trânsito **anunciará os prefixos** da rede downstream para o resto da Internet. Isso significa que, se o AS "A" for um provedor de trânsito para o AS "B", o AS "A" dirá a todos os seus vizinhos BGP: "Eu posso alcançar os prefixos do AS B."
    - **Recebimento de Prefixo:** O provedor de trânsito **receberá os prefixos** de todos os seus vizinhos BGP (sejam eles outros provedores de trânsito, pares ou clientes) e os anunciará para a rede downstream. O AS "B" (cliente) receberá uma "tabela de roteamento completa" ou uma rota padrão (default route) do AS "A", permitindo-lhe alcançar qualquer destino.
    - **Atributos BGP (LOCAL_PREF, AS_PATH):**
        - **Preferência de Saída:** A rede downstream (cliente) geralmente configurará seu BGP para dar uma **alta `LOCAL_PREF`** às rotas aprendidas de seu provedor de trânsito. Isso garante que o tráfego de saída do cliente use o caminho pago, a menos que uma rota mais específica ou preferível seja aprendida via peering.
        - **AS_PATH:** Quando o provedor de trânsito anuncia os prefixos de seu cliente, ele adiciona seu próprio AS ao `AS_PATH`, o que é normal.

### 2. Contratos de Emparelhamento (Peering Agreements)

- **O que é:** Um contrato de emparelhamento ocorre quando duas redes concordam em **trocar tráfego diretamente entre si sem custo**. O objetivo do peering é trocar tráfego que tem um destino ou origem _dentro_ da rede do parceiro de peering, ou nas redes de seus respectivos clientes. Ele _não_ oferece acesso à Internet completa. Se o AS "X" é par do AS "Y", eles trocarão tráfego para os prefixos que eles próprios originam e para os prefixos de seus clientes. Eles _não_ trocarão tráfego que se destine a terceiros, que não sejam seus clientes.
    
- **Analogia:** É como se duas empresas de telefonia concorrentes concordassem em não cobrar uma da outra pelas chamadas entre seus próprios clientes. Eles não estão dando acesso à rede mundial de telefonia um ao outro, apenas a seus próprios clientes.
    
- **Tipos de Peering:**
    
    - **Peering Público:** Ocorre em pontos de troca de tráfego (IXPs - Internet Exchange Points), onde muitas redes se conectam a uma infraestrutura compartilhada para emparelhar com outras redes.
    - **Peering Privado:** Envolve uma conexão direta e dedicada (um ou mais links) entre duas redes em um ou mais locais.
- **Impacto no BGP:**
    
    - **Anúncios de Prefixo:** As redes de peering **anunciarão entre si apenas seus próprios prefixos** e os **prefixos de seus clientes**. Eles _não_ anunciarão os prefixos que aprenderam de seus provedores de trânsito ou de outros pares, pois isso violaria o contrato de peering (seria "transitar" tráfego de terceiros sem pagamento).
    - **Recebimento de Prefixo:** As redes de peering **receberão apenas os prefixos** que o parceiro de peering origina ou de seus clientes diretos.
    - **Atributos BGP (LOCAL_PREF, AS_PATH):**
        - **Preferência de Saída:** As redes frequentemente configuram seu BGP para dar uma **alta `LOCAL_PREF`** às rotas aprendidas de seus pares, pois isso permite que o tráfego seja trocado diretamente e sem custo, evitando o uso do link de trânsito pago. Isso é um forte incentivo financeiro.
        - **AS_PATH:** O `AS_PATH` é atualizado normalmente, adicionando o AS do parceiro.

### Como a Relação Trânsito/Peering Impacta a Seleção de Rota do BGP

O processo de seleção de rota do BGP é fortemente influenciado pelas relações comerciais:

1. **Preferência de Clientes:** As redes BGP geralmente priorizam rotas de seus **clientes** (a quem eles fornecem trânsito) em detrimento de rotas de seus pares ou provedores de trânsito. Isso ocorre porque o cliente está pagando pelo serviço.
    
2. **Preferência de Pares (Peering):** Após as rotas de clientes, as redes geralmente preferem as rotas aprendidas de seus **pares**. A rota através de um par é "gratuita" (custo zero por tráfego, apenas o custo da interconexão), o que a torna preferível a pagar um provedor de trânsito. Essa preferência é tipicamente implementada usando o atributo `LOCAL_PREF` no BGP.
    
3. **Preferência de Trânsito:** Por último, se uma rota não puder ser alcançada via cliente ou par, a rede usará seus **provedores de trânsito**. Estes são o "último recurso" para a conectividade global, mas também são os caminhos pelos quais se paga por volume de tráfego.
    

**Exemplo Prático:**

Imagine o AS X (você), o AS A (seu provedor de trânsito) e o AS B (seu parceiro de peering).

- Você quer enviar tráfego para a Sub-rede Z.
- Você aprende sobre a Sub-rede Z de ambos:
    - Via AS A (seu provedor de trânsito): `AS_PATH = (AS A, AS C, AS Z)`
    - Via AS B (seu parceiro de peering): `AS_PATH = (AS B, AS D, AS Z)`
- Se o AS B _realmente_ originasse a Sub-rede Z, ou se a Sub-rede Z fosse cliente do AS B, então:
    - Você provavelmente configuraria uma `LOCAL_PREF` mais alta para a rota via AS B (parceiro de peering) do que para a rota via AS A (provedor de trânsito).
    - Isso faria com que o tráfego para a Sub-rede Z saísse via AS B, economizando dinheiro, pois você não paga pelo tráfego trocado com seus pares.

### Em Resumo:

Os contratos de emparelhamento e de trânsito são o que impulsiona o BGP e a economia da Internet. Eles determinam quais prefixos são anunciados, para quem, e com quais atributos. As redes manipulam os atributos BGP (especialmente `LOCAL_PREF` e `AS_PATH`) para implementar suas políticas de roteamento que refletem suas relações comerciais, priorizando tráfego gratuito (peering) sobre tráfego pago (trânsito) e garantindo que o tráfego de seus clientes seja sempre preferencialmente roteado. Compreender esses contratos é essencial para entender por que o BGP toma as decisões que toma na Internet.