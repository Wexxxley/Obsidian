
#Concluded 

---

[3_ Socket e portas](../../2_Redes%20de%20computadores/3_Camada%20de%20Transporte/3_%20Socket%20e%20portas.md)
### 1. Socket
O socket é definido como uma **abstração** que serve como ponto de destino para a comunicação entre processos em um sistema distribuído.

1. **Endereçamento e Associação:** Para que um processo possa receber mensagens, seu soquete deve estar associado a dois elementos essenciais:
	 - ==(Endereço IP da máquina, Porta do processo)==

2. **Exclusividade da Porta:** Mensagens enviadas a um endereço IP e número de porta específicos só podem ser recebidas pelo processo cujo soquete esteja associado.

3. **Protocolos Associados:** Cada soquete está sempre associado a um **protocolo em particular**: **UDP** (User Datagram Protocol) ou **TCP** (Transmission Control Protocol).

[1_Protocolos da camada de transporte da internet](../../2_Redes%20de%20computadores/3_Camada%20de%20Transporte/1_Protocolos%20da%20camada%20de%20transporte%20da%20internet.md)
#### **1.1 Comunicação por Datagrama (UDP)**
- O soquete UDP é usado para enviar e receber datagramas **sem garantia de entrega**.
- Um servidor associa seu soquete a uma **porta de serviço conhecida** para que os clientes possam enviar mensagens para lá.
- O método de recebimento (`receive`) geralmente é **bloqueante** e, além da mensagem, retorna o endereço IP e a porta de origem, permitindo que o destinatário envie uma resposta.
- O UDP é de **um para um**.

#### **1.2 Comunicação por Fluxo (TCP)**
A tupla ==(local IP, local porta, remoto IP, remoto porta)== identifica  a conexão.

- É usado o soquete de fluxo (stream) 
- Na conexão, um processo atua como **cliente** e o outro como **servidor**.
- O servidor cria um **soquete de "escuta"** , vinculado à porta de serviço, para esperar que os clientes solicitem conexões. O soquete de escuta mantém uma fila de pedidos de conexão recebidos.
- Quando o servidor aceita uma conexão, um **novo soquete de fluxo é criado** especificamente para se comunicar com o cliente, enquanto o soquete de escuta permanece na porta de serviço para aceitar outros pedidos.
- Os dados escritos em um fluxo são mantidos em uma fila no **soquete de destino**. Um processo que tenta ler dados será bloqueado até que os dados estejam disponíveis. Além disso, um processo de escrita pode ser bloqueado pelo controle de fluxo TCP se o soquete no outro lado estiver armazenando o volume máximo permitido de dados.
- **Um para um orientado a conexão**

![](../../attachments/Pasted%20image%2020251009124402.png)

---
### **2. Comunicação Síncrona vs. Assíncrona**

1. **Comunicação Síncrona:** O processo de origem é **bloqueado** até que a operação correspondente, como o recebimento (_receive_) da mensagem, seja concluída. 

2. **Comunicação Assíncrona:** A operação de envio (_send_) é **não bloqueante**. O processo de origem pode continuar a execução assim que a mensagem for copiada para um _buffer_ local. A transmissão da mensagem ocorre em paralelo com o processo de origem.
    - A operação de recebimento em comunicação assíncrona pode ter variantes com e sem bloqueio. Na variante **não bloqueante**, o processo destino continua a execução após executar o `receive`, e o _buffer_ é preenchido em _background_. O processo deve então receber uma notificação de que os dados estão prontos.

---
### 3. Comunicação por Fluxo (Streams)

O modelo de comunicação por fluxo (como o **TCP**) lida com a transmissão e exibição de dados contínuos em tempo real.

- **Controle de Bloqueio:** Os dados gravados em um fluxo são mantidos em uma fila no soquete de destino. Um processo que tenta ler dados será bloqueado até que os dados estejam disponíveis. O processo que escreve também pode ser bloqueado pelo mecanismo de **controle de fluxo TCP** se o soquete no outro lado já estiver armazenando o volume máximo de dados permitido.
- **Uso de Threads:** É comum que um servidor, ao aceitar uma conexão, crie uma **nova _thread_** para se comunicar com o cliente. A vantagem disso é que o servidor pode bloquear enquanto espera por dados (para leitura ou escrita) **sem atrasar outros clientes**.

---
### 4. Comunicação por Datagrama
O termo **datagrama** (como o **UDP**) refere-se a um modo de entrega de dados onde a distribuição de cada pacote é um **procedimento independente**.
- **Características:** Nenhuma configuração é exigida e, uma vez que o pacote é entregue, a rede não mantém mais nenhuma informação sobre ele.
- **Ordem:** Em uma rede baseada em datagramas, uma sequência de pacotes pode seguir rotas diferentes, podendo **chegar fora da sequência** em que foram emitidos.
- **Uso:** Embora datagramas sejam frequentemente usados para fluxos de dados multimídia em tempo real (como quadros de vídeo), a operação `receive` em soquetes de datagrama é tipicamente bloqueante, a não ser que um tempo limite seja configurado.
