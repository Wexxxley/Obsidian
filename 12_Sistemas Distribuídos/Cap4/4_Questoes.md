

---

**O Multicast é**

a. uma especificação de sistemas de comunicação multimídia em redes baseadas em pacotes e que não provê em uma QoS garantida.

<mark style="background: #BBFABBA6;">b. a entrega de informação para múltiplos destinatários simultaneamente onde as mensagens só passam por um _link_ uma única vez. </mark>

c.  um protocolo que determina a qualidade em que o serviço de comunicação deve ter do início ao fim.

d. um protocolo de sinal para estabelecer chamadas e conferências por meio de redes via utilizando o protocolo IP.

e. um protocolo do protocolo IP com a função de controlar os membros de um grupo de _multicast_ IP.

---

**_Sockets_ são uma abstração que permite a comunicação entre processos computacionais. Eles podem ser do tipo Datagrama, que faz uso do protocolo UDP, ou do tipo _Stream_, que faz uso do protocolo TCP. Sobre esta abstração é correto afirmar que**


a.  o sistema de coleta de lixo dos modernos sistemas operacionais, como o Linux, o Windows e o MacOSX, fecham automaticamente os _sockets_ criados pelos processos quando esses são finalizados.

b. a primitiva _receive_ nos _sockets_ do tipo Datagrama tem como um dos seus parâmetros o endereço do processo remoto remetente.

<mark style="background: #BBFABBA6;">c.  a primitiva _send_ nos sockets do tipo _Stream_ não precisa ter como parâmetro o endereço do processo para o qual a mensagem deve ser enviada pois uma conexão entre os processos deve ser previamente estabelecida. </mark>

d. um processo que deseja trocar mensagem com outros processos pode ter no máximo duas portas, uma de saída para enviar as suas mensagens de solicitação de serviço e uma de entrada para receber as mensagens de resultado dos serviços solicitados.

---

**Na figura a seguir, estão representados os processos e sockets de comunicação entre três computadores.**

![](https://cdn.tecconcursos.com.br/figuras/5b990698-ee8d-4956-b97d-966c9daccdbc)

Com base na representação acima, é **INCORRETO** afirmar que

a. um processo servidor recebe requisições em uma determinada porta e cria _threads_ para tratar separadamente cada requisição recebida de um ou mais processos clientes simultaneamente.

b. uma aplicação pode utilizar tanto _sockets_ UDP quanto TC

c. uma aplicação que utiliza TCP possui dois _sockets_: um receptivo para receber o pedido de conexão TCP do cliente e outro de conexão para trocar mensagens.

<mark style="background: #BBFABBA6;">d. uma aplicação Internet utiliza portas fixas para identificar os processos clientes.</mark>

Os **servidores** usam portas fixas (bem conhecidas) para que os clientes possam encontrá-los. Os **clientes**, por outro lado, geralmente não usam portas fixas. Um cliente vincula seu soquete a **qualquer porta local livre**.

e. um _Socket_, identificado por um número de porta de dezesseis bits, é uma interface de software para que aplicações enviem e/ou recebam mensagens, usando os protocolos TCP ou UDP da camada de transporte.

---
**Em relação a comunicações baseadas em _Socket_ na linguagem de programação Java, são feitas as seguintes afirmações**

**I.** Caso aconteça algum erro de entrada/saída ao fechar o socket, uma exceção do tipo _SocketException_ irá ocorrer.

operações `send` e `receive` podem disparar uma `IOException`

**II.** Um objeto da classe _InetAddress_ contém um endereço IP.

**III.** A classe _DatagramSocket_ vincula o aplicativo a uma porta para transmissão de datagrama.

Estão corretas as afirmativas

Escolha uma opção:

a. **I** e **II** apenas.

b. **I**, **II** e **III**. 

c. **I** e **III** apenas.

<mark style="background: #BBFABBA6;">d. **II** e **III** apenas.
</mark>

---

**Sobre classes de endereço de IP em sua versão 4 (IPv4), é correto afirmar que**

a.  classe A: primeiro bit do endereço IP é 1.

b. classe B: primeiros dois bits do endereço IP são 11.

c. classe D (multicast): primeiros três bits do endereço IP são 101.

<mark style="background: #BBFABBA6;">d.  classe C: primeiros três bits do endereço IP são 110. </mark>

e.  classe E: primeiros quatro bits do endereço IP são 1010.

| Classes | Intervalo do Primeiro Octeto | Padrão dos Primeiros Bits | Uso Principal        |
| :------ | :--------------------------- | :------------------------ | :------------------- |
| **A**   | 0 - 127      (128)           | `0`xxxxxxx                | Grandes redes        |
| **B**   | 128 - 191 (64)               | `10`xxxxxx                | Médias/Grandes redes |
| **C**   | 192 - 223 (32)               | `110`xxxxx                | Pequenas redes       |
| **D**   | 224 - 239 (16)               | `1110`xxxx                | Multicast            |
| **E**   | 240 - 255 (16)               | `1111`xxxx                | Experimental/Testes  |
As classes são calculadas com base no primeiro octeto de bits.

---

**Marque a alternativa correta em relação às comunicações baseadas em _socket_ da linguagem Java:**

a. Essa comunicação permite ao aplicativo visualizar a rede como se fosse um _applet_.

b. Os _sockets_ de datagrama através do protocolo UDP utilizam o serviço orientado para conexão.

c. Os _sockets_ de fluxo através do protocolo TCP fornecem um serviço sem conexão.

d. O _socket_ é uma construção de software que representa a parte intermediária de uma conexão.

<mark style="background: #BBFABBA6;">e. Essa comunicação permite ao aplicativo visualizar a rede como se fosse uma entrada/saída de arquivo.</mark>

Para usar um `Socket` TCP, o programador obtém um `InputStream` e um `OutputStream`. Essas são as mesmas classes abstratas do pacote `java.io` usadas para ler e escrever em arquivos. Isso permite ao aplicativo tratar a rede como se fosse um arquivo, lendo dados dela (`read`) e escrevendo dados para ela (`write`).