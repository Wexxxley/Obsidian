
#Concluded 

---

A ideia é permitir que um programa cliente chame um procedimento em um servidor remoto como se fosse um procedimento local. O sistema de RPC, atuando como middleware, oculta todos os detalhes complexos da distribuição, como:

- Empacotamento dos parâmetros da chamada em uma mensagem.
- A transmissão dessa mensagem de requisição ao servidor.
- O recebimento da mensagem de resposta.
- Desempacotamento dos resultados.

---
### **1. Programação com Interfaces**
Em sistemas distribuídos, os módulos (cliente e servidor) executam-se em processos distintos. O servidor fornece uma **interface de serviço**.
    
- Para permitir que programas escritos em linguagens diferentes se comuniquem, os sistemas RPC usam uma **IDL - Interface Definition Language**. Uma IDL é uma notação neutra usada para definir os procedimentos, seus parâmetros (in , out ou inout) e seus tipos de retorno.
    
- Como os processos estão em espaços de endereçamento diferentes, a passagem de parâmetros por "referência" não é suportada. Os parâmetros são passados por valor.   

---
### **2. Semânticas**

**Semântica talvez:** O cliente envia a requisição apenas uma vez. Ele não tenta retransmitir se a resposta não chegar. 

**Semântica Pelo Menos Uma Vez :** O cliente retransmite a requisição até receber uma resposta. O servidor _não_ tem um filtro para detectar requisições duplicadas. O cliente sabe se receber uma resposta que o procedimento foi executado **uma ou mais vezes**.

**Semântica No Máximo Uma Vez**: O cliente retransmite a requisição, MAS o servidor usa filtragem de duplicatas (checando um ID de requisição) e um histórico de respostas. O cliente sabe ao receber uma resposta que o procedimento foi executado **exatamente uma vez**.

---
### 3. Transparência
O objetivo original da RPC era fornecer transparência de acesso e localização, fazendo com que a chamada remota fosse sintaticamente idêntica a uma chamada local. No entanto, essa transparência não é total. Chamadas remotas são fundamentalmente diferentes das locais:

- Estão sujeitas a falhas de rede e de processos remotos.      
- Têm uma latência significativamente maior.  
- Não suportam passagem de parâmetros por referência. 

Portanto, o consenso atual é que, embora a _sintaxe_ da chamada deva ser transparente, a interface
do serviço remoto deve deixar claro que se trata de uma operação distribuída, por exemplo, disparando exceções específicas de rede.

---
#### **Implementação de RPC**

A RPC é implementada usando componentes de software gerados automaticamente a partir da definição da IDL:

![600](../../attachments/Pasted%20image%2020251107141415.png)

- **Client Stub**: Um procedimento que é executado no cliente. Ele se parece com o procedimento remoto real, mas sua única função é empacotar os argumentos em uma mensagem de requisição e enviá-la ao servidor. Em seguida, ele espera pela resposta, desempacota os resultados e os retorna ao programa cliente.
    
- **Módulo de Comunicação**: Lida com a transmissão de mensagens entre o cliente e o servidor, implementando a semântica de chamada desejada (ex: retransmissões).
    
- **Despachante**: Executado no servidor. Ele recebe a mensagem de requisição, examina o identificador do procedimento e chama o server stub.
    
- **Server stub**: Um procedimento no servidor. Sua função é desempacotar os argumentos da mensagem de requisição, chamar o procedimento de serviço real (a implementação) e, em seguida, empacotar os resultados em uma mensagem de resposta para enviar de volta ao cliente.
