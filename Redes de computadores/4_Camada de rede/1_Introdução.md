
---

### **1.1 Intro**
O papel da camada de rede é  simples transportar pacotes de um hospedeiro remetente a um hospedeiro destinatário.  
![[Pasted image 20250522195127.png]]
**Comutação**: mover pacotes da entrada do roteador para a saída apropriada.
**Roteamento**: determinar a rota a ser seguida pelos pacotes desde a origem até o destino por meio de algoritmos de roteamento.

Cada roteador tem uma **tabela de repasse**. Um roteador repassa um pacote examinando o valor de um campo no cabeçalho do pacote e então utiliza esse valor para indexar sua tabela de repasse. O resultado indica para qual das interfaces de enlace do roteador o pacote deve ser repassado.
![[Pasted image 20250522195536.png]]

---
### 2. Por dentro de roteador

![[Pasted image 20250522195916.png]]


