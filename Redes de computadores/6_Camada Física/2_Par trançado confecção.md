
---

### **1. As Normas de Cores: T568A e T568B**
Para que os dispositivos de rede consigam se comunicar, os 8 fios dentro de um cabo de rede precisam ser organizados em uma ordem específica no conector RJ-45. Existem duas normas principais para isso, a **T568A** e a **T568B**. 

**Padrão T568A**
![[Pasted image 20250703104648.png|600]]

![[Pasted image 20250703105455.png|550]]
A partir dessas duas normas, criamos os principais de cabos: o **Cabo Direto** e o **Cabo Crossover**.

---
### **2. Tipos de Conexão e Cabos**
A necessidade de cabos diferentes vem da forma como os dispositivos enviam e recebem dados. 
- **Adaptadores de PCs e Roteadores:** Usam pinos 1 e 2 para transmitir e pinos 3 e 6 para receber.
- **Switches e Hubs:** Usam os pinos 1 e 2 para receber e os pinos 3 e 6 para transmitir.

![[Pasted image 20250703105106.png]]

    

#### 1. Conexão PC para Switch/Hub (Cabo Direto)

Para conectar um PC (MDI) a um Switch (MDI-X), precisamos que os pinos de transmissão do PC cheguem aos pinos de recepção do Switch. Como os dispositivos já têm essa inversão interna, usamos um **Cabo Direto (Straight-Through)**.

- **O que é:** Um cabo direto tem a **mesma norma nas duas pontas** (geralmente T568B nas duas).
    
- **Como funciona:** O pino 1 do PC se conecta ao pino 1 do Switch, o pino 2 ao 2, e assim por diante. A comunicação funciona porque o Switch já espera receber dados nos pinos em que o PC está transmitindo.
    

Imagem 2: Conexão PC-Switch com Cabo Direto

(Ilustração mostrando um PC conectado a um Switch com um cabo de rede. Ambas as pontas do cabo mostram a pinagem idêntica, T568B, alinhando TX do PC com RX do Switch).

PC (TX pinos 1,2) -----> (RX pinos 1,2) Switch

PC (RX pinos 3,6) <----- (TX pinos 3,6) Switch

#### 2. Conexão PC para PC (Cabo Crossover)

Se você tentar conectar dois PCs (MDI para MDI) com um cabo direto, a comunicação falha. Ambos estariam tentando transmitir nos mesmos pinos (1 e 2) e receber nos mesmos pinos (3 e 6). É como duas pessoas tentando falar ao mesmo tempo no mesmo canal e ninguém escutando.

Para resolver isso, usamos um **Cabo Crossover (Cruzado)**.

- **O que é:** Um cabo crossover tem a norma **T568A em uma ponta** e a **T568B na outra**.
    
- **Como funciona:** Ao usar normas diferentes, os fios verde e laranja são cruzados. Isso faz com que os pinos de transmissão (TX) de um PC sejam conectados diretamente aos pinos de recepção (RX) do outro PC, e vice-versa.
    

Imagem 3: Conexão PC-PC com Cabo Crossover

(Ilustração mostrando dois PCs conectados. Uma ponta do cabo tem a pinagem T568A e a outra T568B. Fica claro que os pinos de transmissão de um PC estão fisicamente direcionados para os pinos de recepção do outro).

PC 1 (TX pinos 1,2) --Cabo Crossover--> (RX pinos 1,2) PC 2

PC 1 (RX pinos 3,6) <--Cabo Crossover-- (TX pinos 3,6) PC 2

A mesma lógica se aplica para conectar dois switches ou dois hubs diretamente: também seria necessário um cabo crossover.

---

### A Solução Moderna: Auto MDI/MDI-X

A necessidade de ter dois tipos de cabos sempre foi uma fonte de confusão. Era comum um técnico de rede chegar a um local e não ter o cabo certo para a conexão necessária.

Para eliminar esse problema, foi criada a tecnologia **Auto MDI/MDI-X (Automatic Medium-Dependent Interface Crossover)**.

**O que é:** É um recurso presente na grande maioria dos equipamentos de rede modernos (placas de rede, switches, roteadores). A porta de rede consegue **detectar automaticamente** o tipo de dispositivo que está na outra ponta e qual tipo de cabo está sendo usado (direto ou crossover).

**Como funciona:** Ao conectar um cabo, a porta analisa os sinais e, se necessário, **cruza ou descruza os pares de transmissão e recepção via software**, internamente. Ela se configura para funcionar como MDI ou MDI-X, o que for necessário para estabelecer a comunicação.

**Benefício Prático:** Com o Auto MDI/MDI-X, **você pode usar um cabo de rede direto (o mais comum) para praticamente qualquer conexão**:

- PC para Switch
    
- PC para PC
    
- Switch para Switch
    

A tecnologia faz o ajuste automaticamente, tornando o **cabo crossover obsoleto** na maioria das situações do dia a dia. Você só vai realmente precisar de um cabo crossover hoje se estiver trabalhando com equipamentos de rede muito antigos que não possuem essa funcionalidade.