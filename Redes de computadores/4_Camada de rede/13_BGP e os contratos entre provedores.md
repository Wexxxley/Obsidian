

---
### **1. Contratos de Trânsito** 
- Um contrato de trânsito ocorre quando uma rede (geralmente menor) paga a outra rede (geralmente maior) para ter acesso à _Internet completa_. O provedor concorda em levar o tráfego da rede para _qualquer_ destino na Internet, e também a entregar o tráfego de _qualquer_ lugar da Internet para a rede menor.

- **Impacto no BGP:**
    - O provedor **anunciará os prefixos** da rede menor para o resto da Internet.
    - O provedor **receberá os prefixos** de todos os seus vizinhos e os anunciará para a rede downstream. O AS "B" (cliente) receberá uma "tabela de roteamento completa" ou uma rota padrão (default route) do AS "A", permitindo-lhe alcançar qualquer destino.
    - **Atributos BGP (LOCAL_PREF, AS_PATH):**
        - **Preferência de Saída:** A rede downstream (cliente) geralmente configurará seu BGP para dar uma **alta `LOCAL_PREF`** às rotas aprendidas de seu provedor de trânsito. Isso garante que o tráfego de saída do cliente use o caminho pago, a menos que uma rota mais específica ou preferível seja aprendida via peering.
        - **AS_PATH:** Quando o provedor de trânsito anuncia os prefixos de seu cliente, ele adiciona seu próprio AS ao `AS_PATH`, o que é normal.


![[Pasted image 20250606103652.png]]

### 2. Contratos de Emparelhamento (Peering)
- Um contrato de emparelhamento ocorre quando duas redes concordam em **trocar tráfego diretamente entre si sem custo**. Ele _não_ oferece acesso à Internet completa. Se o AS "X" é par do AS "Y", eles trocarão tráfego para os prefixos que eles próprios originam e para os prefixos de seus clientes. Eles _não_ trocarão tráfego que se destine a terceiros.

- **Tipos de Peering:**
    - **Peering Público:** Ocorre em pontos de troca de tráfego, onde muitas redes se conectam a uma infraestrutura compartilhada para emparelhar com outras redes.
    - **Peering Privado:** Envolve uma conexão direta e dedicada.

- **Impacto no BGP:**
    - As redes de peering **anunciarão entre si apenas seus próprios prefixos** e os **prefixos de seus clientes**. Eles _não_ anunciarão os prefixos que aprenderam de seus provedores de trânsito ou de outros pares, pois isso violaria o contrato.
