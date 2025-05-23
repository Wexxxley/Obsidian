
---
### **1.1 Intro**
O papel da camada de rede é  simples transportar pacotes de um hospedeiro remetente a um hospedeiro destinatário.  

**Comutação**: mover pacotes da entrada do roteador para a saída apropriada.
**Roteamento**: determinar a rota a ser seguida pelos pacotes desde a origem até o destino por meio de algoritmos de roteamento.
![[Pasted image 20250522195127.png]]**1. Internetworking**: A camada de rede torna possível que **dispositivos em diferentes redes físicas** se comuniquem, formando uma **"internet" de redes**.
**2. Endereçamento**: Define os **endereços lógicos**usados para identificar dispositivos na rede.
**3. Roteamento**: Decide o **caminho** que os pacotes devem seguir para chegar ao destino.
**4. Encapsulamento**: Consiste em **envolver os dados** com cabeçalhos.
- VPN usa encapsulamento na camada de rede para **criar túneis criptografados** sobre redes públicas.
- Exemplo:
    - Um pacote IP original é **encapsulado dentro de outro pacote IP**, com um novo cabeçalho que aponta para o servidor VPN.

**5. Fragmentação**: Quando um pacote IP é **muito grande para ser transmitido** em uma rede menor, ele é **dividido em fragmentos menores**.

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

---
#### **1.2.1 Funções da porta de entrada**
![[Pasted image 20250522200227.png]]
1. **Terminação de linha**: Responsável por **receber sinais físicos** vindos de uma interface de rede. Converte esses sinais em **bits** digitais para que possam ser interpretados pelas camadas superiores.
2. **Processamento de enlace:** Aqui ocorre o **desencapsulamento da camada de enlace**. Extrai o quadro recebido e verifica seu conteúdo. Remove o cabeçalho da camada de enlace.
3. **Consulta, repasse, fila**: Esta é a parte da camada de rede. O roteador consulta sua tabela de roteamento para decidir para onde o pacote deve ser enviado e repassa o pacote para a interface correta.
    - Pode **armazenar temporariamente (enfileirar)** se a saída estiver ocupada.

---
#### **1.2.2 Elemento de comutação**
![[Pasted image 20250522201358.png]]

É por meio do elemento de comutação que os pacotes são comutados (isto é, repassados) de uma porta de entrada para uma porta de saída. A comutação pode ser realizada de inúmeras maneiras:
##### 1. **Comutação via Memória**
- Os pacotes entram por uma interface.
- São **copiados para a memória central** do roteador.
- A CPU acessa os dados, processa o cabeçalho e determina a interface de saída.
- O pacote é então **reenviado da memória para a porta de saída**.

- Simples de implementar.
- Limitado pela **largura de banda da memória** e pela **velocidade do processador**.
- Pode causar gargalo em tráfego alto, pois apenas um pacote pode ser lido/escrito por vez.
##### 2. **Comutação via Barramento**
- Um **barramento compartilhado** conecta todas as interfaces.
- Quando um pacote chega à interface, ele é colocado no barramento e enviado para a interface de saída.
- **Apenas uma transmissão pode ocorrer por vez** no barramento. ==Problema de contenção==

- Mais rápido que o modelo com memória.
- Ainda há limitação: **uma única transferência por vez** no barramento.
##### 3. **Crossbar** 
- Usa uma **malha de conexões** que permite **várias transmissões simultâneas**, desde que não haja conflito de destino.
- Cada entrada (A, B, C) pode se conectar diretamente com cada saída (X, Y, Z), dependendo da disponibilidade.
- Ainda pode ocorrer o ==Problema de contenção== quando existem duas transmissões para a mesma interface.

- Muito mais escalável e rápida.    
- Permite **transmissões paralelas**, ideal para **roteadores de alta performance**.
- Mais cara e complexa de implementar.

##### **Bloqueio head of the line** 
Problema que acontece quando o primeiro pacote de uma fila impede que outros pacotes atrás dele sejam transmitidos, mesmo que esses pacotes possam ser encaminhados.

Imagine uma fila de pacotes aguardando para sair por diferentes interfaces. Porém, **a fila é comum (FIFO)**, ou seja, os pacotes têm que sair na ordem de chegada.
1. O **pacote 1** está no início da fila e precisa sair pela **porta X**, que está **ocupada**.
2. O **pacote 2** está logo atrás e quer ir para a **porta Y**, que está **livre**.

Resultado: a **fila inteira fica bloqueada**, mesmo tendo pacotes que poderiam ser transmitidos.

---
#### **1.2.3 Processamento de saída**
![[Pasted image 20250522203955.png]]
##### 1.**Fila (gerenciamento de buffer)**
- Quando o pacote chega à saída, ele **pode ter que esperar** se a interface de transmissão estiver ocupada.
- Se o buffer estiver cheio, os pacotes **podem ser descartados**.
##### 2. **Processamento de enlace
- Aqui, o pacote IP é **encapsulado novamente** em um **quadro de camada de enlace**.
##### 3. **Terminação de linha**
- A etapa final: **conversão dos dados digitais** para sinais físicos.