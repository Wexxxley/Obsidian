
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
- **PCs e Roteadores (MDI):** Usam pinos 1 e 2 para transmitir e pinos 3 e 6 para receber.
- **Switches e Hubs (MDI-X):** Usam os pinos 1 e 2 para receber e os pinos 3 e 6 para transmitir.
#### **2.1 Conexão PC para Switch/Hub (Cabo Direto)**
Para conectar um PC (MDI) a um Switch (MDI-X), precisamos que os pinos de transmissão do PC cheguem aos pinos de recepção do Switch. Como os dispositivos já têm essa inversão interna, usamos um **Cabo Direto**. Um cabo direto tem a **mesma norma nas duas pontas**.
![[Pasted image 20250703185928.png|400]]
#### **2.1 Conexão PC para PC (Cabo Crossover)**
Se você tentar conectar dois PCs com um cabo direto, a comunicação falha. Ambos estariam tentando transmitir nos mesmos pinos (1 e 2) e receber nos mesmos pinos (3 e 6). 
- Um cabo crossover tem a norma **T568A em uma ponta** e a **T568B na outra**.
![[Pasted image 20250703105106.png|400]]
#### **2.3 Auto MDI/MDI-X**
A necessidade de ter dois tipos de cabos sempre foi uma fonte de confusão. Para eliminar esse problema, foi criada a tecnologia **Auto MDI/MDI-X**.

**O que é:** É um recurso presente na grande maioria dos equipamentos de rede modernos (placas de rede, switches, roteadores). A porta de rede consegue **detectar automaticamente** o tipo de dispositivo que está na outra ponta e qual tipo de cabo está sendo usado (direto ou crossover).

**Como funciona:** Ao conectar um cabo, a porta analisa os sinais e, se necessário, **cruza ou descruza os pares de transmissão e recepção via software**, internamente. Ela se configura para funcionar como MDI ou MDI-X, o que for necessário para estabelecer a comunicação.

**Benefício Prático:** Com o Auto MDI/MDI-X, **você pode usar um cabo de rede direto (o mais comum) para praticamente qualquer conexão**:

- PC para Switch
    
- PC para PC
    
- Switch para Switch
    

A tecnologia faz o ajuste automaticamente, tornando o **cabo crossover obsoleto** na maioria das situações do dia a dia. Você só vai realmente precisar de um cabo crossover hoje se estiver trabalhando com equipamentos de rede muito antigos que não possuem essa funcionalidade.