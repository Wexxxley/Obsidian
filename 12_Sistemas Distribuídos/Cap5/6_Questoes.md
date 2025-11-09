

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
