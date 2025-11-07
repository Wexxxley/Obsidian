
#Concluded 

---

Este capítulo foca nos mecanismos que permitem que processos em diferentes computadores se comuniquem invocando operações uns nos outros. 

O livro destaca três paradigmas principais de invocação remota que:

1. **Protocolos de Requisição-Resposta**: Forma mais básica de interação cliente-servidor, onde um cliente envia uma mensagem de requisição e espera por uma mensagem de resposta. 
    
2. **Chamada de Procedimento Remoto (RPC - Remote Procedure Call)**: O objetivo é permitir que um cliente chame um procedimento em um servidor remoto de forma transparente, como se fosse uma chamada de procedimento local.
    
3. **Invocação a Método Remoto (RMI - Remote Method Invocation)**: Similar à RPC, permite que um objeto invoque métodos de um objeto que está em outro processo.

Esses mecanismos formam uma camada de **middleware** que oculta a complexidade da passagem de mensagens e da comunicação de rede.
![](../../attachments/Pasted%20image%2020251029104835.png)