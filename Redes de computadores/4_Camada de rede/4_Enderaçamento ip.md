

---

Um hospedeiro em geral tem apenas um único enlace com a rede; quando o IP no hospedeiro quer enviar um datagrama, ele o faz por meio desse enlace. **A fronteira entre o hospedeiro e o enlace físico é denominada interface**. Agora considere um roteador e suas interfaces. Como a tarefa de um roteador é receber um datagrama em um enlace e repassá-lo a algum outro enlace, ele necessariamente estará ligado a dois ou mais enlaces. A fronteira entre o roteador e qualquer um desses enlaces também é denominada uma interface. Assim, um roteador tem múltiplas interfaces, uma para cada enlace. Como todos os hospedeiros e roteadores podem enviar e receber datagramas IP, o IP exige que cada interface tenha seu próprio endereço IP. Desse modo, **um endereço IP está tecnicamente associado com uma interface**, e não com um hospedeiro 

![[Pasted image 20250524113525.png]]

==Cada endereço IPv4 tem comprimento de 32 bits (equivalente a 4 bytes).==

Cada interface em cada hospedeiro e roteador da Internet global tem de ter um endereço IP  exclusivo. Contudo, os endereços não podem ser escolhidos de qualquer maneira. Uma parte do endereço IP de uma interface será determinada pela sub-rede à qual ela está conectada.

**Sub-rede:** uma **sub-rede** é definida como um conjunto de interfaces de rede que são interconectadas e que compartilham uma parte comum do endereço IP. 