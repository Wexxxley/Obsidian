
---

### **1.1 Intro**
O papel da camada de rede é  simples transportar pacotes de um hospedeiro remetente a um hospedeiro destinatário.  
![[Pasted image 20250522195127.png]]
**Comutação**: mover pacotes da entrada do roteador para a saída apropriada.
**Roteamento**: determinar a rota a ser seguida pelos pacotes desde a origem até o destino por meio de algoritmos de roteamento.

Cada roteador tem uma **tabela de repasse**. Um roteador repassa um pacote examinando o valor de um campo no cabeçalho do pacote e então utiliza esse valor para indexar sua tabela de repasse. O resultado indica para qual das interfaces de enlace do roteador o pacote deve ser repassado.
![[Pasted image 20250522195536.png]]

---
### **1.2 Por dentro de roteador**

![[Pasted image 20250522195916.png]]
Quatro componentes de um roteador podem ser identificados: 
- Portas de entrada.
- Elemento de comutação. O elemento de comutação conecta as portas de entrada do roteador às suas portas de saída. 
- Portas de saída. Uma porta de saída armazena os pacotes que foram repassados a ela através do elemento de comutação e, então, os transmite até o enlace de saída, realizando as funções necessárias da camada de enlace e da camada físico
- Processador de roteamento. O processador de roteamento executa os protocolos de roteamento, mantém as tabelas de roteamento e as informações de estado do enlace, e calcula a tabela de repasse para o roteador. 

#### **1.2.1 Funções da porta de entrada**
![[Pasted image 20250522200227.png]]
1. **Terminação de linha**: Responsável por **receber sinais físicos** vindos de uma interface de rede. Converte esses sinais em **bits** digitais para que possam ser interpretados pelas camadas superiores.
2. **Processamento de enlace:** Aqui ocorre o **desencapsulamento da camada de enlace**. Extrai o quadro recebido e verifica seu conteúdo. Remove o cabeçalho da camada de enlace.
3. **Consulta, repasse, fila**: Esta é a parte da camada de rede. O roteador consulta sua tabela de roteamento para decidir para onde o pacote deve ser enviado e repassa o pacote para a interface correta.
    - Pode **armazenar temporariamente (enfileirar)** se a saída estiver ocupada.

### 🔹 4. **Elemento de comutação (switching fabric)**

- É o "núcleo" do roteador.
    
- **Transfere fisicamente os pacotes** entre as interfaces de entrada e saída.