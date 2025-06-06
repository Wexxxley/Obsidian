
#Concluded 

---

O papel da camada de rede é transportar pacotes de um hospedeiro remetente a um hospedeiro destinatário.  

**Comutação**: processo de mover pacotes da entrada do roteador para a saída apropriada.
**Roteamento**:  processo de determinar a rota a ser seguida pelos pacotes desde a origem até o destino por meio de algoritmos de roteamento.

![[Pasted image 20250522195127.png]]**1. Internetworking**: A camada de rede torna possível que **dispositivos em diferentes redes** se comuniquem, formando uma **"internet" de redes**.
**2. Endereçamento**: Define os **endereços lógicos** usados para identificar dispositivos na rede.
**3. Roteamento**: Decide o **caminho** que os pacotes devem seguir para chegar ao destino.
**4. Encapsulamento**: Consiste em **envolver os dados** com cabeçalhos.
- **VPN** usa encapsulamento na camada de rede para **criar túneis criptografados** sobre redes públicas. Um pacote IP original é **encapsulado dentro de outro pacote IP**, com um novo cabeçalho que aponta para o servidor VPN.
**5. Fragmentação**: Quando um pacote IPv4 é **muito grande para ser transmitido** em uma enlace, ele é dividido em fragmentos menores.

Cada roteador tem uma **tabela de repasse**. Um roteador repassa um pacote examinando o destino do pacote. O resultado indica para qual das interfaces de enlace do roteador o pacote deve ser repassado.
![[Pasted image 20250522195536.png]]
