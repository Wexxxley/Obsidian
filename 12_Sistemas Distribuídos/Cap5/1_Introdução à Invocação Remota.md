
#Concluded 

---

Este capítulo foca nos mecanismos que permitem que processos (ou entidades como objetos e serviços) em diferentes computadores se comuniquem invocando operações uns nos outros. 

O livro destaca três paradigmas principais de invocação remota que serão examinados:

1. **Protocolos de Requisição-Resposta**: É a forma mais básica de interação cliente-servidor, onde um cliente envia uma mensagem de requisição e espera por uma mensagem de resposta2. É a base para os outros dois paradigmas.
    
2. **Chamada de Procedimento Remoto (RPC - Remote Procedure Call)**: Este é um avanço significativo que estende a ideia familiar de uma "chamada de procedimento" para um ambiente distribuído. O objetivo é permitir que um cliente chame um procedimento em um servidor remoto de forma transparente, como se fosse uma chamada de procedimento local3.
    
3. **Invocação a Método Remoto (RMI - Remote Method Invocation)**: Similar à RPC, mas aplicada ao modelo de programação orientada a objetos4. Permite que um objeto em um processo invoque métodos de um objeto que está em outro processo5.
    

Esses mecanismos formam uma camada de **middleware** que oculta a complexidade da passagem de mensagens e da comunicação de rede, fornecendo uma base mais simples para a construção de aplicações e serviços distribuídos6.

---

A seguir, o livro detalha os **Protocolos de Requisição-Resposta**.

Quando quiser continuar, é só digitar **next**.
Esses mecanismos formam a camada do **middleware** que fica imediatamente acima da comunicação básica entre processos (como UDP e TCP).
![](attachments/Pasted%20image%2020251029104835.png)