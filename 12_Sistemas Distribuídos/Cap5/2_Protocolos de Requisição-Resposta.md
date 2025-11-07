
#Concluded 

---
Um **protocolo de requisição-resposta** é projetado especificamente para suportar a interação típica cliente-servidor. Na sua forma normal, a comunicação é:
- **síncrona**: o processo cliente envia uma requisição e fica bloqueado até que a resposta do servidor chegue.
- **confiável**: pois a mensagem de resposta do servidor atua como uma confirmação de que a requisição foi recebida.

#### **Primitivas de Comunicação**

1. **`doOperation` (Cliente)**: Usada pelo cliente para invocar a operação remota. Ela envia a mensagem de requisição e bloqueia, esperando pela mensagem de resposta.

2. **`getRequest` (Servidor)**: Usada pelo servidor para receber uma mensagem de requisição de um cliente.

3. **`sendReply` (Servidor)**: Usada pelo servidor para enviar a mensagem de resposta de volta ao cliente que fez a requisição.

![](../../attachments/Pasted%20image%2020251029105559.png)
#### **Estrutura da Mensagem**

- **Tipo de Mensagem**: Request ou Resposta.
- **ID da Requisição**: Um identificador único gerado pelo cliente para cada requisição. O servidor copia esse ID, permitindo que o cliente associe a resposta à requisição correta.
- **Referência Remota**: Identifica o objeto ou serviço remoto sendo invocado.
- **ID da Operação**: Identifica qual operação específica deve ser executada.
    
![](../../attachments/Pasted%20image%2020251029105832.png)

#### **Tratamento de Falhas (sobre UDP)**

Se o protocolo for implementado sobre UDP  ele herda as falhas do UDP, ou seja, as mensagens podem ser perdidas. Para fornecer uma comunicação confiável, o protocolo de requisição-resposta deve tratar dessas falhas:

- **Timeouts e Retransmissões**: A operação `doOperation` no cliente usa um tempo limite ao esperar pela resposta. Se o tempo esgotar, o cliente assume que a mensagem (de requisição ou de resposta) se perdeu e retransmite a mensagem de requisição.
    
- **Filtragem de Requisições Duplicadas**: Como o cliente pode retransmitir requisições, o servidor pode receber a mesma requisição múltiplas vezes. O servidor usa o `requestId` da mensagem para detectar e descartar duplicatas.
    
- **Respostas Perdidas e o Histórico**: Se a mensagem de _resposta_ se perder, o cliente fará um timeout e retransmitirá a requisição. O servidor irá detectar isso como uma duplicata.
    - Se a operação for **idempotente**, o servidor pode simplesmente reexecutá-la e enviar a nova resposta.
    - Se a operação não for idempotente (como "sacar R$ 100"), o servidor armazena a resposta em um cache de respostas). Ao receber uma requisição duplicada, ele não reexecuta a operação, apenas retransmite a resposta salva no histórico.

#### **Estilos de Protocolo**

- **R (Request)**: Apenas uma mensagem de requisição é enviada (sem resposta). 
    
- **RR (Request-Reply)**: O padrão normal, com uma requisição seguida por uma resposta.
    
- **RRA (Request-Reply-Acknowledge Reply)**: Uma terceira mensagem (confirmação da resposta) é enviada pelo cliente de volta ao servidor. Isso permite que o servidor saiba que a resposta foi recebida e que ele pode descartar essa resposta do seu histórico.
