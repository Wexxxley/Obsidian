
---

Máquina A (na Rede 1) Quer Falar com Máquina B (na Rede 2)

1. **A cria o pacote IP com origem A, destino B.**
    - A máquina A, ao verificar o endereço IP de destino, percebe que B _não está na mesma rede. 
    - A envia o pacote para seu **gateway padrão**. Então, A envia uma Requisição ARP perguntando: "Quem tem o IP `111.111.111.110`?".
    - O roteador R responde com seu endereço MAC para aquela interface. 
    - A pode constuir o quadro agora. O **endereço MAC de destino** do quadro será o MAC do **roteador** (o próximo salto).
    
2. **A camada de enlace de R recebe o quadro.**        
    - O roteador verifica o endereço MAC de destino do quadro. Como é o seu próprio endereço MAC, ele aceita o quadro.    
    - O roteador desencapsula o quadro. Ele agora tem o **datagrama IP original**.
    - O roteador examina o **endereço IP de destino**. Ele consulta sua **tabela de roteamento**. A tabela de roteamento dirá por qual de suas interfaces o pacote deve sair.
    - O roteador envia uma Requisição ARP na rede de destino perguntando: "Quem tem o IP de B?". A máquina B responde com seu endereço MAC.    
    - Com o endereço MAC de B em mãos, o roteador R agora cria um **novo quadro**. O **endereço MAC de destino** deste _novo_ quadro será o MAC da máquina **B**. O **endereço MAC de origem** será o MAC da interface do próprio roteador roteador.