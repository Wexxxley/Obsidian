

---
**Descreva as maneiras pelas quais o protocolo de requisição-resposta mascara a heterogeneidade dos sistemas operacionais e das redes de computador.**

- **Mascarando a Heterogeneidade de SO's:** O protocolo mascara essas diferenças usando empacotamento e uma representação externa de dados padronizada. Antes de enviar uma mensagem, o processo de empacotamento converte os dados do formato local da máquina para um formato externo padronizado. O processo receptor, então, desempacota, convertendo-os desse formato padrão de volta para o seu próprio formato local. Isso garante que os dados possam ser trocados, independentemente do hardware ou SO de cada máquina.
    
- **Mascarando a Heterogeneidade de Rede:** O protocolo de requisição-resposta em si não mascara diretamente as redes. Em vez disso, ele **utiliza os protocolos Internet subjacentes (como IP, TCP e UDP)**, que são os responsáveis por mascarar as diferenças entre as diversas tecnologias de rede (como Ethernet, WiFi, etc.).

---
![](../../attachments/Pasted%20image%2020251109064901.png)

---
![](../../attachments/Pasted%20image%2020251109065125.png)

- **Protocolo RR:** Este protocolo usa a **confirmação implícita**. O servidor é forçado a manter a última resposta de um cliente armazenada até que esse cliente decida fazer uma _nova_ requisição (o que pode demorar muito ou nunca acontecer) ou até que um timeout expire.
    
- **Protocolo RRA:** Este protocolo usa a **confirmação explícita**. Como o cliente envia uma mensagem de confirmação, o servidor sabe exatamente quando a resposta pode ser descartada. O server armazena a resposta por um curto período.

---

**Suponha que o protocolo RRA esteja em uso. Por quanto tempo os servidores devem manter**
**dados de resposta não confirmados? Os servidores devem enviar a resposta repetidamente, em uma tentativa de receber uma confirmação?**

- **Por quanto tempo os servidores devem manter os dados?** O servidor deve manter os dados da resposta em seu histórico até que a mensagem de confirmação do cliente seja recebida. Se essa confirmação for perdida, o servidor geralmente manterá a resposta até que um **timeout** expire.
    
- **Os servidores devem enviar a resposta repetidamente para obter uma confirmação?** **Não.** Se a resposta original se perder, o cliente (que não a recebeu) fará um _timeout_ e retransmitirá a **requisição** original. O servidor, ao receber essa requisição duplicada, apenas reenvia a resposta.

---

![](../../attachments/Pasted%20image%2020251109065936.png)
![](../../attachments/Pasted%20image%2020251109070021.png)

---
![](../../attachments/Pasted%20image%2020251109070416.png)

**Semanticas rpc**

**Semântica talvez:** O cliente envia a requisição apenas uma vez. Ele não tenta retransmitir se a resposta não chegar. 

**Semântica Pelo Menos Uma Vez :** O cliente retransmite a requisição até receber uma resposta. O servidor _não_ tem um filtro para detectar requisições duplicadas. O cliente sabe se receber uma resposta que o procedimento foi executado **uma ou mais vezes**.

**Semântica No Máximo Uma Vez**: O cliente retransmite a requisição, MAS o servidor usa filtragem de duplicatas (checando um ID de requisição) e um histórico de respostas. O cliente sabe ao receber uma resposta que o procedimento foi executado **exatamente uma vez**.


---
![](../../attachments/Pasted%20image%2020251109070618.png)

---
**Um protocolo de requisição-resposta é implementado em um serviço de comunicação com falhas por omissão para fornecer semântica de invocação pelo menos uma vez. No primeiro caso, o desenvolvedor presume um sistema assíncrono distribuído. No segundo caso, o desenvolve-dor presume que o tempo máximo para a comunicação e a execução de um método remoto é T. De que maneira esta última suposição simplifica a implementação?**

Com base no livro "Sistemas Distribuídos: Conceitos e Projeto", a suposição de um tempo máximo T (um sistema síncrono) simplifica a implementação porque torna a **detecção de falhas menos ambígua**.

Em um sistema **assíncrono**, se um cliente não recebe uma resposta e seu _timeout_ expira, a causa é **ambígua**. O processo pode ter entrado em colapso, estar lento ou, ainda, as mensagens podem não ter chegado. O desenvolvedor precisa _adivinhar_ um valor de _timeout_ adequado, correndo o risco de retransmitir desnecessariamente.

Em um sistema **síncrono** (com tempo máximo T), a lentidão máxima já está incluída no valor de T. Portanto, se o _timeout_ T expirar e a resposta não chegar, o desenvolvedor pode descartar a lentidão como causa. Ele sabe que uma falha por perda de mensagem ou colapso do servidor ocorreu, tornando a decisão de retransmitir (para garantir a semântica de "pelo menos uma vez") muito mais simples.


