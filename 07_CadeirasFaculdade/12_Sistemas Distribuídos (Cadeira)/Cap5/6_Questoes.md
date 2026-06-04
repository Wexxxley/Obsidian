

---
**O User Datagram Protocol (UDP) é um protocolo de transporte leve e sem conexão utilizado em redes de computadores. Ele oferece um serviço de entrega de dados não confiável, o que significa que não há garantia de entrega ou ordenação dos pacotes. Assinale a opção que apresenta exemplos de protocolos que utilizam o UDP Escolha uma opção:** 

a. SNMP (Simple Network Management Protocol), HTTP (Hypertext Transfer Protocol) e RIP (Routing Information Protocol). 

b. SMTP (Simple Mail Transfer Protocol), DNS (Domain Name System) e HTTP (Hypertext Transfer Protocol). 

<mark style="background: #BBFABBA6;">c. RPC (Remote Procedure Call), SNMP (Simple Network Management Protocol) e RIP (Routing Information Protocol). </mark>

d. DNS (Domain Name System), IMAP (Internet Message Access Protocol) e SNMP (Simple Network Management Protocol). 

e. DNS (Domain Name System), RPC (Remote Procedure Call) e SMTP (Simple Mail Transfer Protocol)

**HTTP:** Precisa de entrega confiável e ordenada para carregar páginas e, portanto, é implementado sobre TCP.
**SMTP:** A entrega de e-mail precisa ser confiável. Portanto, o SMTP usa TCP.
**IMAP:** Protocolo de e-mail que requer uma conexão confiável e, portanto, usa TCP.

**RPC:** Foi projetada para ser flexível e "Os implementadores têm a opção de usar chamadas de procedimento remoto sobre UDP ou TCP".
**SNMP:** É um protocolo de gerenciamento que prioriza a velocidade e o baixo custo (sem conexão), sendo um usuário clássico do UDP.
**RIP:** É um protocolo de roteamento que envia atualizações periódicas; a perda de uma atualização não é catastrófica.

---

**No contexto de RPC (Remote Procedure Call), considerando uma chamada remota de procedimento (procedure) via rede de um cliente a um servidor, um dos papeis de objetos do tipo skeleton é:** 

a. oferecer um mecanismo de persistência abstrato para os procedimentos que executam no lado do servidor, salvando informações que precisam ser persistidas em um banco de dados de forma transparente. 

b. fornecer ao chamador do procedimento remoto, no lado do cliente, uma lista de servidores ativos que disponibilizam esse procedimento, permitindo que o cliente decida qual servidor chamar. 

c. abrir uma conexão TCP com o servidor para trafegar os dados da chamada remota. 

d. serializar os parâmetros da chamada remota, no cliente, para envio via rede ao servidor. 

<mark style="background: #BBFABBA6;">e. traduzir dados recebidos da chamada remota, convertendo esses dados em uma chamada de procedimento local no servidor.</mark>

![600](../../../attachments/Pasted%20image%2020251107141415.png)

**Server stub/skeleton**: Sua função é desempacotar os argumentos da mensagem de requisição, chamar o procedimento de serviço real e, em seguida, empacotar os resultados em uma mensagem de resposta para enviar de volta ao cliente.

---
São exemplos de implementações de mecanismos de RPC (Remote Procedure Call): 

a. DCOM, WWW, HTTP, CORBA 
b. RAM,RMI, IRC, HTTP 
c. FTP, HTTP,RM-ODP,TCP/IP 
d. HTTP, FTP, CORBA, TCP/IP 
<mark style="background: #BBFABBA6;">e. CORBA,RMI,DCOM, RM-ODP </mark>

**RMI (Remote Method Invocation):** Extensão do RPC para o mundo dos objetos distribuídos.
**CORBA:** Arquitetura de middleware que "permite às aplicações se comunicarem umas com as outras" através de um Object Request Broker, que é uma implementação da ideia de RMI/RPC.
**DCOM e RM-ODP:** Eles são conceitualmente da mesma família de `CORBA` e `RMI`. 

---
**Assinale a alternativa que indica todas as afirmativas corretas.** 

**1.SOAP é baseado em XML e possui 3 partes: um envelope; um conjunto de regras e uma mensagem.** 

**2.SOAP pode ser utilizado sobre HTTP ou até mesmo SMTP.** 

**3.Pode-se implementar RPC (Remote Procedure Call) em webservices utilizando SOAP.** 

a. São corretas as afirmativas 1, 2 e 3. 
b. São corretas apenas as afirmativas 1 e 3. 
c. São corretas apenas as afirmativas 1 e 2. 
<mark style="background: #BBFABBA6;">d. São corretas apenas as afirmativas 2 e 3. </mark>
e. É correta apenas a afirmativa 1.

**SOAP (Simple Object Access Protocol)** é um protocolo que permitir a comunicação entre aplicações pela Internet. Ele usa XML para empacotar mensagens. Um cliente pode enviar uma mensagem SOAP para um servidor para executar uma operação, e o servidor retorna a resposta em outra mensagem SOAP.

- **1. INCORRETA.** Uma mensagem SOAP possui três partes: **envelope**, **cabeçalho** (opc) e **corpo**. 
    
- **2. CORRETA.** normalmente, o protocolo SOAP era baseado apenas em HTTP, mas a versão atual é projetada para usar uma variedade de protocolos de transporte, incluindo SMTP, TCP ou UDP".
    
- **3. CORRETA.** O livro afirma que o SOAP suporta interações requisição-resposta usando pares de mensagens e "especificando como irá representar as operações, seus argumentos e resultados". 

---

**O modelo OSI divide as funções das redes de computadores em sete camadas de abstração. São elas: a definição do modelo, definição dos protocolos de camada e a seleção de perfis funcionais. Uma das camadas pode ser definida da seguinte maneira: "Esta camada é responsável por iniciar e encerrar conexões de rede. A definição se refere à camada: Escolha uma opção:** 

a. <mark style="background: #BBFABBA6;">sessão</mark> 
b. rede 
c. transporte 
d. física

---
**Relacione os seguintes middlewares com suas respectivas definições.** 

1. RPC. 
2. CORBA 
3. JAVA RMI 
4. JAVA EJB 

(**CORBA**) É um middleware que fornece um modelo de objetos distribuído e um conjunto de serviços para a comunicação entre objetos remotos. 
(**RPC**) É um protocolo que permite a comunicação entre processos em execução em máquinas diferentes. 
(**JAVA EJB**) É um framework que fornece um modelo de componentes para a criação de aplicações distribuídas. 
(**JAVA RMI**) É um framework que permite a criação de objetos remotos em Java. 

a. 2 – 1 – 3 – 4. 
<mark style="background: #BBFABBA6;">b. 2 – 1 – 4 – 3.  </mark>
c. 3 – 2 – 4 – 1. 
d. 2 – 3 – 1 – 4. 
e. 1 – 2 – 4 – 3.

---
**O Network File System version 4 (NFSv4) foi aprimorado para reduzir a quantidade de trocas de mensagens entre cliente e servidor. Sem prévio contato com o servidor, um cliente é capaz de combinar as operações de busca, abertura e leitura de um arquivo em uma requisição usando uma:** 

a. descrição ASN.1 (Abstract Syntax Notation One.) composta 
b. única SPC (Single Procedure Call) composta 
c. query SQL (Structured Query Language.) composta 
<mark style="background: #BBFABBA6;">d. única RPC (Remote Procedure Call) composta </mark>
e. descrição XML (eXtended Mark-up Language.) composta

O NFSv4 permite **combinar várias operações** (busca, abertura, leitura) em uma **única requisição**. Isso é uma otimização do protocolo RPC, mas o mecanismo fundamental de invocação continua sendo uma RPC.

---

**O sistema de objetos distribuídos RMI (remote method invocation) permite que objetos Java e objetos não Java sejam acessados remotamente como se fossem locais.**

<mark style="background: #BBFABBA6;">Falso</mark>

- O **RMI Java** é apresentado como um sistema de linguagem única. O livro afirma que "o uso de RMI Java é restrito ao desenvolvimento baseado em Java.
- O **CORBA** é apresentado como a solução "multilinguagem" projetada para permitir a interoperabilidade entre objetos escritos em diferentes linguagens.

---
**Chamadas de procedimento remoto (RPC remote procedure call) são uma forma de comunicação entre processos na qual diferentes processos têm diferentes espaços de endereço.** 

<mark style="background: #BBFABBA6;">Verdadeiro</mark>

Um "processo" é uma unidade de gerenciamento de recursos que possui seu próprio espaço de endereçamento. O livro reforça essa separação na seção sobre RPC ao explicar por que a passagem de parâmetros por referência (ponteiros de memória) não é suportada: "os endereços de um processo não são válidos em outro processo remoto".

---
**Descreva as maneiras pelas quais o protocolo de requisição-resposta mascara a heterogeneidade dos sistemas operacionais e das redes de computador.**

- **Mascarando a Heterogeneidade de SO's:** O protocolo mascara essas diferenças usando uma representação externa de dados padronizada. Antes de enviar uma mensagem, o processo de empacotamento converte os dados do formato local da máquina para um formato externo padronizado. O processo receptor, então, desempacota, convertendo-os desse formato padrão de volta para o seu próprio formato local. Isso garante que os dados possam ser trocados, independentemente do hardware ou SO de cada máquina.
    
- **Mascarando a Heterogeneidade de Rede:** O protocolo de requisição-resposta em si não mascara diretamente as redes. Em vez disso, ele **utiliza os protocolos Internet subjacentes (como IP, TCP e UDP)**, que são os responsáveis por mascarar as diferenças entre as diversas tecnologias de rede (como Ethernet, WiFi, etc.).

---
![](../../../attachments/Pasted%20image%2020251109064901.png)

---
![](../../../attachments/Pasted%20image%2020251109065125.png)

- **Protocolo RR:** Este protocolo usa a **confirmação implícita**. O servidor é forçado a manter a última resposta de um cliente armazenada até que esse cliente decida fazer uma _nova_ requisição (o que pode demorar muito ou nunca acontecer) ou até que um timeout expire.
    
- **Protocolo RRA:** Este protocolo usa a **confirmação explícita**. Como o cliente envia uma mensagem de confirmação, o servidor sabe exatamente quando a resposta pode ser descartada. 

---

**Suponha que o protocolo RRA esteja em uso. Por quanto tempo os servidores devem manter dados de resposta não confirmados? Os servidores devem enviar a resposta repetidamente, em uma tentativa de receber uma confirmação?**

- **Por quanto tempo os servidores devem manter os dados?** O servidor deve manter os dados da resposta em seu histórico até que a mensagem de confirmação do cliente seja recebida. Se essa confirmação for perdida, o servidor geralmente manterá a resposta até que um **timeout** expire.
    
- **Os servidores devem enviar a resposta repetidamente para obter uma confirmação?** **Não.** Se a resposta original se perder, o cliente (que não a recebeu) fará um _timeout_ e retransmitirá a **requisição** original. 

---

![](../../../attachments/Pasted%20image%2020251109065936.png)
![](../../../attachments/Pasted%20image%2020251109070021.png)

---
![](../../../attachments/Pasted%20image%2020251109070416.png)

**Semanticas rpc**

**Semântica talvez:** O cliente envia a requisição apenas uma vez. Ele não tenta retransmitir se a resposta não chegar. 

**Semântica Pelo Menos Uma Vez :** O cliente retransmite a requisição até receber uma resposta. O servidor _não_ tem um filtro para detectar requisições duplicadas. O cliente sabe se receber uma resposta que o procedimento foi executado **uma ou mais vezes**.

**Semântica No Máximo Uma Vez**: O cliente retransmite a requisição, MAS o servidor usa filtragem de duplicatas (checando um ID de requisição) e um histórico de respostas. O cliente sabe ao receber uma resposta que o procedimento foi executado **exatamente uma vez**.


---
![](../../../attachments/Pasted%20image%2020251109070618.png)

---
**Um protocolo de requisição-resposta é implementado em um serviço de comunicação com falhas por omissão para fornecer semântica de invocação pelo menos uma vez. No primeiro caso, o desenvolvedor presume um sistema assíncrono distribuído. No segundo caso, o desenvolve-dor presume que o tempo máximo para a comunicação e a execução de um método remoto é T. De que maneira esta última suposição simplifica a implementação?**

A suposição de um tempo máximo T (um sistema síncrono) simplifica a implementação porque torna a **detecção de falhas menos ambígua**.

Em um sistema **assíncrono**, se um cliente não recebe uma resposta e seu _timeout_ expira, a causa é **ambígua**. O processo pode ter entrado em colapso, estar lento ou, ainda, as mensagens podem não ter chegado. O desenvolvedor precisa _adivinhar_ um valor de _timeout_ adequado, correndo o risco de retransmitir desnecessariamente.

Em um sistema **síncrono** (com tempo máximo T), a lentidão máxima já está incluída no valor de T. Portanto, se o _timeout_ T expirar e a resposta não chegar, o desenvolvedor pode descartar a lentidão como causa. Ele sabe que uma falha por perda de mensagem ou colapso do servidor ocorreu, tornando a decisão de retransmitir (para garantir a semântica de "pelo menos uma vez") muito mais simples.

---

**O cliente demora 5 milissegundos para computar os argumentos de cada requisição, e o servidor demora 10 milissegundos para processar cada requisição. O tempo de processamento do sistema operacional local para cada operação de envio ou recepção é de 0,5 milissegundos, e o tempo que a rede leva para transmitir cada mensagem de requisição ou resposta é de 3 milissegundos. O empacotamento ou desempacotamento demora 0,5 milissegundos por mensagem.

**Calcule o tempo que leva para o cliente gerar e retornar duas requisições: 
(i) se ele tiver só uma thread; 
(ii) se ele tiver duas threads que podem fazer requisições concorrentes em um único processador. 

**Você pode ignorar os tempos de troca de contexto. Há necessidade de invocação assíncrona se os processos cliente e servidor forem programados com múltiplas threads?**


Primeiro, precisamos calcular o tempo total para uma única requisição ser concluída.

1. **Cliente (Preparação):**
    - Computar argumentos: 5,0 ms
    - Empacotar (Marshalling): 0,5 ms
    - SO (Envio): 0,5 ms
        
2. **Rede (Ida):**
    - Transmissão da Requisição: 3,0 ms
        
3. **Servidor (Processamento):**
    - SO (Recepção): 0,5 ms
    - Desempacotar (Unmarshalling): 0,5 ms
    - Processar a requisição: 10,0 ms
    - Empacotar (Marshalling) Resposta: 0,5 ms
    - SO (Envio): 0,5 ms
        
4. **Rede (Volta):**
    - Transmissão da Resposta: 3,0 ms
        
5. **Cliente (Finalização):**
    - SO (Recepção): 0,5 ms
    - Desempacotar (Unmarshalling) Resposta: 0,5 ms
        

**Tempo total para uma RMI = 6,0 + 3,0 + 12,0 + 3,0 + 1,0 = 25,0 ms**


Se o cliente tiver apenas uma thread, as operações são puramente sequenciais. 
- Tempo da Requisição 1: 25,0 ms
- Tempo da Requisição 2: 25,0 ms
    
**Tempo Total (i) = 25,0 ms + 25,0 ms = 50,0 ms**

No cenário com duas threads, temos dois recursos principais que são gargalos: a **CPU do Cliente** (que é única e compartilhada pelas duas threads) e a **CPU do Servidor** (que também é única e processa sequencialmente).

Uma thread (T1) fará a Requisição 1 (Req 1) e a outra (T2) fará a Requisição 2 (Req 2). Elas podem sobrepor a computação do cliente com a E/S (rede) e o processamento do servidor.

**Linha do Tempo:**
- `T=0`: **T1 (CPU Cliente)** começa a computar Req 1. (Duração: 5,0 ms)
- `T=5`: **T1 (CPU Cliente)** começa a Empacotar/Enviar Req 1. (Duração: 1,0 ms)
- `T=6`: Req 1 entra na Rede (E/S). (Chegará no servidor em T=9).
- `T=6`: A CPU do Cliente está livre (T1 está bloqueada em E/S). **T2 (CPU Cliente)** começa a computar Req 2. (Duração: 5,0 ms)
- `T=9`: Req 1 chega ao Servidor. **CPU Servidor** começa a processar Req 1. (Duração: 12,0 ms)
- `T=11`: **T2 (CPU Cliente)** começa a Empacotar/Enviar Req 2. (Duração: 1,0 ms)
- `T=12`: Req 2 entra na Rede (E/S). (Chegará no servidor em T=15).
- `T=15`: Req 2 chega ao Servidor, mas a CPU do Servidor está ocupada com a Req 1. Req 2 entra na **fila** do servidor. 
- `T=21`: **CPU Servidor** termina Req 1. Resposta 1 entra na Rede (E/S). (Chegará no cliente em T=24).
- `T=21`: **CPU Servidor** (agora livre) começa a processar Req 2 (da fila). (Duração: 12,0 ms)
- `T=24`: Resposta 1 chega ao Cliente. **T1 (CPU Cliente)** começa a Receber/Desempacotar. (Duração: 1,0 ms)
- `T=25`: **Requisição 1 está completa.**
- `T=33`: **CPU Servidor** termina Req 2. Resposta 2 entra na Rede (E/S). (Chegará no cliente em T=36).
- `T=36`: Resposta 2 chega ao Cliente. **T2 (CPU Cliente)** começa a Receber/Desempacotar. (Duração: 1,0 ms)
- `T=37`: **Requisição 2 está completa.**
    

O tempo total é o tempo até que a _última_ thread (T2) termine seu trabalho.

**Tempo Total (ii) = 37,0 ms**

---
### **Há necessidade de invocação assíncrona?**

A questão é se a **invocação assíncrona** (onde a chamada `doOperation` retorna imediatamente, sem bloquear a thread) é _necessária_ se o cliente e o servidor já são multi-thread.

**Não, não é estritamente _necessária_ para alcançar a concorrência, mas é um modelo de programação alternativo para alcançá-la.**

- **Concorrência com Threads (Nosso cálculo ii):** Como vimos, o cliente pode alcançar a concorrência (e sobrepor E/S e computação) simplesmente disparando **duas chamadas síncronas (bloqueantes)** em duas threads separadas. O Sistema Operacional gerencia a execução da T2 na CPU do cliente enquanto a T1 está bloqueada esperando pela rede.
    
- **Concorrência com Invocação Assíncrona:** Uma _única thread_ de cliente poderia usar invocações assíncronas. Ela dispararia a Req 1 (que retornaria imediatamente) e, em seguida, dispararia a Req 2 (que também retornaria imediatamente). Essa única thread ficaria, então, responsável por esperar (através de _polling_ ou _callbacks_) que ambas as respostas chegassem.
    

O resultado final de desempenho (37,0 ms) seria o mesmo em ambos os modelos, pois o gargalo é o servidor processando as requisições sequencialmente.

Portanto, em um cliente multi-thread, você **pode** usar chamadas síncronas (bloqueantes) em threads separadas para obter concorrência. A invocação assíncrona é um modelo diferente que atinge o mesmo objetivo (geralmente com menos sobrecarga de gerenciamento de threads) e seria a solução _necessária_ se o cliente fosse _single-threaded_.

