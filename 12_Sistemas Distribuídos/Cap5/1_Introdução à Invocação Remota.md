
#Concluded 

---

O livro destaca três abordagens principais que serão examinadas no capítulo:

1. **Protocolos de Requisição-Resposta**: Eles estabelecem um padrão sobre a passagem de mensagens para suportar a troca de uma mensagem de requisição seguida por uma mensagem de resposta. São a base para as outras duas técnicas mais sofisticadas.
    
2. **Chamada de Procedimento Remoto (RPC - Remote Procedure Call)**: A ideia é permitir que um programa cliente chame um procedimento em um programa servidor de forma transparente, como se fosse uma chamada local. O sistema RPC oculta os detalhes da comunicação.
    
3. **Invocação a Método Remoto (RMI - Remote Method Invocation)**: É a extensão da RPC para o mundo dos objetos distribuídos. Permite que um objeto em um processo invoque métodos de um objeto que está em outro processo, usando uma sintaxe semelhante à invocação de método local.    

Esses mecanismos formam a camada do **middleware** que fica imediatamente acima da comunicação básica entre processos (como UDP e TCP).
![](attachments/Pasted%20image%2020251029104835.png)