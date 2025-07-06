
---
# Socket e porta

Sockets são uma interface de programação de aplicativos ==API que permite a comunicação entre processos em diferentes computadores através de uma rede==. Eles são usados para enviar e receber dados entre processos e permitem que os desenvolvedores criem programas que possam se comunicar por meio de uma rede de computadores.

**Porta**: É um número (de 0 a 65535) que serve para identificar qual programa/processo está usando uma conexão dentro de um computador.
- O endereço IP leva até o computador.
- A porta diz qual o programa em execução que vai enviar ou receber algo.
- Portas conhecidas: 0-1023 (reservadas para serviços padrão como HTTP, FTP.
- As portas acima de 1023 são usadas para comunicações temporárias.

**Exemplo**
Digamos que você está acessando um site. A conexão é feita assim:
Seu navegador cria um socket local com:
- IP da sua máquina e Porta aleatória local.

E se conecta a um socket remoto com:

- IP do servidor e Porta do serviço.  

Esse par ==(local IP, local porta, remoto IP, remoto porta)== identifica  a conexão.

---
# Programação com sockets

**Socket UDP (Sem Conexão)**: Um socket UDP é identificado por dois valores:
- IP de destino e Porta de destino.  

![Pasted image 20250509132053](../../attachments/Pasted%20image%2020250509132053.png)

**Socket TCP (com  Conexão):** Um socket TCP é identificado por quatro valores:
- IP de origem, Porta de origem, IP de destino e Porta de destino.  

![Pasted image 20250509132033](../../attachments/Pasted%20image%2020250509132033.png)

As principais funções necessárias para o uso de sockets incluem: 

1. **socket():** cria um novo socket e retorna seu descritor de arquivo. (GERAL)
2. **bind():** associa o socket a um endereço IP e porta local. (GERAL)
3. **listen():** coloca o socket em modo de escuta e aguarda por **conexões**. (usado no TCP)
4. **accept():** aceita uma **conexão** e cria um novo socket para comunicação. (usado no TCP)
5. **connect():** inicia uma **conexão** de saída com um servidor. (usado no TCP) 
6. **close():** fecha o socket e libera todos os recursos associados a ele. (GERAL)
7. **sendto():** Envia um datagrama especificando o endereço. (usado no UDP)
8. **recvfrom**(): Recebe um datagrama e guarda o endereço do emisssor (usado no UDP)
9. **write():** Escreve dados em uma **conexão** (usado no TCP)
10. **read()**: Lê dados de uma **conexão** (usado no TCP)