

---
Um **protocolo de requisição-resposta** é projetado especificamente para suportar a interação típica cliente-servidor. Na sua forma normal, a comunicação é:
- **síncrona**: o processo cliente envia uma requisição e fica bloqueado até que a resposta do servidor chegue.
- **confiável**: pois a mensagem de resposta do servidor atua como uma confirmação de que a requisição foi recebida.

#### **Primitivas de Comunicação**

1. **`doOperation` (Cliente)**: Usada pelo cliente para invocar a operação remota. Ela envia a mensagem de requisição e bloqueia, esperando pela mensagem de resposta.

2. **`getRequest` (Servidor)**: Usada pelo servidor para receber uma mensagem de requisição de um cliente.

3. **`sendReply` (Servidor)**: Usada pelo servidor para enviar a mensagem de resposta de volta ao cliente que fez a requisição.

![](attachments/Pasted%20image%2020251029105559.png)

### **Estrutura da Mensagem**

- **Tipo de Mensagem**: Request ou Resposta.
- **ID da Requisição**: Um identificador único gerado pelo cliente para cada requisição. O servidor copia esse ID na resposta correspondente, permitindo que o cliente associe a resposta à requisição correta e descarte respostas de requisições antigas ou duplicadas.
- **Referência Remota**: Identifica o objeto ou serviço remoto sendo invocado.
- **ID da Operação**: Identifica qual operação específica deve ser executada.
    
![](attachments/Pasted%20image%2020251029105832.png)

#### **Tratamento de Falhas (sobre UDP)**

Se o protocolo for implementado sobre UDP (datagramas), ele herda as falhas do UDP, ou seja, as mensagens podem ser perdidas12. Para fornecer uma comunicação confiável, o protocolo de requisição-resposta deve tratar dessas falhas:

- **Timeouts e Retransmissões**: A operação `doOperation` no cliente usa um tempo limite (timeout) ao esperar pela resposta13. Se o tempo esgotar, o cliente assume que a mensagem (de requisição ou de resposta) se perdeu e retransmite a mensagem de requisição14.
    
- **Filtragem de Requisições Duplicadas**: Como o cliente pode retransmitir requisições, o servidor pode receber a mesma requisição múltiplas vezes15. O servidor usa o `requestId` da mensagem para detectar e descartar duplicatas, garantindo que a operação não seja executada mais de uma vez indevidamente16.
    
- **Respostas Perdidas e o Histórico**: Se a mensagem de _resposta_ se perder, o cliente fará um timeout e retransmitirá a requisição17. O servidor irá detectar isso como uma duplicata.
    
    - Se a operação for **idempotente** (pode ser executada várias vezes com o mesmo resultado, como ler um valor), o servidor pode simplesmente reexecutá-la e enviar a nova resposta18.
        
    - Se a operação não for idempotente (como "sacar R$ 100"), o servidor não deve reexecutá-la. Nesses casos, o servidor armazena a resposta em um **"histórico"** (cache de respostas)19. Ao receber uma requisição duplicada, ele não reexecuta a operação, apenas retransmite a resposta salva no histórico20.
        

#### **Estilos de Protocolo**

O livro menciona três estilos de protocolos de troca, dependendo das garantias necessárias21:

- **R (Request)**: Apenas uma mensagem de requisição é enviada (sem resposta). Tem semântica "talvez".
    
- **RR (Request-Reply)**: O padrão normal, com uma requisição seguida por uma resposta.
    
- **RRA (Request-Reply-Acknowledge Reply)**: Uma terceira mensagem (confirmação da resposta) é enviada pelo cliente de volta ao servidor. Isso permite que o servidor saiba que a resposta foi recebida e que ele pode descartar essa resposta do seu histórico22.
    

#### **HTTP como Exemplo**

O **HTTP** (Protocolo de Transferência de Hipertexto) é um exemplo proeminente de um protocolo de requisição-resposta23. Ele é geralmente implementado sobre **TCP** (e não UDP), o que simplifica o projeto, pois o TCP já cuida da perda de mensagens e da duplicação24. Versões modernas como o HTTP 1.1 usam **conexões persistentes** (reutilizam a mesma conexão TCP para várias trocas de requisição-resposta) para amortizar o custo de estabelecer a conexão25.

---

A seguir, o livro aborda a **Chamada de Procedimento Remoto (RPC)**, que é construída sobre esses protocolos de requisição-resposta.

Quando quiser continuar, é só digitar **next**.
    


1. **Cliente:** Monta uma mensagem contendo a operação desejada e os dados necessários. 
2. **Cliente:** Envia essa mensagem pela rede para o endereço do servidor (IP e porta).
3. **Cliente:** Entra em estado de espera (bloqueio).
4. **Servidor:** Está em um "loop de escuta". Ao receber a mensagem, ele a interpreta.
5. **Servidor:** Executa a ação solicitada.
6. **Servidor:** Monta uma mensagem de resposta contendo o resultado.
7. **Servidor:** Envia a resposta de volta ao cliente.
8. **Cliente:** Recebe a resposta, "desbloqueia" e continua sua execução.

---
### **2. 
---
### 3. Uso com o UDP

Implementar um protocolo de requisição-resposta diretamente sobre datagramas UDP pode ser mais eficiente do que usar TCP para interações simples, pois evita sobrecargas desnecessárias do TCP:

- **Confirmações:** São redundantes, já que a resposta do servidor confirma a requisição.
- **Estabelecimento de Conexão**: O TCP exige trocas extras de mensagens para estabelecer e fechar uma conexão.
- **Controle de Fluxo**: Geralmente desnecessário para invocações que passam apenas pequenos argumentos e resultados.

Quando implementado sobre UDP, o protocolo herda suas falhas (mensagens podem ser perdidas ou chegar fora de ordem) e precisa lidar com elas e também com falhas de processo:

- **Timeouts**: A operação `doOperation` no cliente usa um timeout ao esperar pela resposta. Se o timeout expirar, a ação mais comum é **retransmitir a mensagem de requisição** várias vezes antes de desistir e relatar um erro.
    
- **Requisições Duplicadas**: Devido às retransmissões, o servidor pode receber a mesma requisição múltiplas vezes. O protocolo deve incluir um mecanismo para que o servidor **detecte e descarte requisições duplicadas**, geralmente usando o `requestId`.
    
- **Respostas Perdidas e Idempotência**: Se a resposta se perder, o cliente retransmitirá a requisição. Se a operação no servidor for **idempotente** (pode ser executada várias vezes com o mesmo efeito que uma única execução), o servidor pode simplesmente reexecutá-la. Se não for idempotente, o servidor precisa manter um **histórico** das respostas enviadas (indexado pelo `requestId`) para poder retransmitir a resposta sem reexecutar a operação.
    

---
### **4. Estilos de Protocolos de Troca (R, RR, RRA)**

- **R (Request)**: Apenas uma mensagem de requisição. Útil quando não há resultado e a confirmação não é necessária.
    
- **RR (Request-Reply)**: O padrão normal, com uma requisição seguida por uma resposta. 
    
- **RRA (Request-Reply-Acknowledge Reply)**: Uma terceira mensagem (confirmação da resposta) é enviada pelo cliente de volta ao servidor. Isso permite que o servidor descarte com segurança as entradas do histórico de respostas.
    
---
### **5. Uso de TCP**

Apesar das vantagens do UDP para casos simples, o TCP é frequentemente usado para implementar protocolos de requisição-resposta:

- Simplifica a implementação, pois o TCP já garante a entrega confiável e ordenada, eliminando a necessidade de retransmissões.
    
- O controle de fluxo do TCP permite a transmissão de argumentos e resultados de tamanho arbitrário.
    
- A sobrecarga da conexão TCP pode ser amortizada se a mesma conexão for reutilizada para múltiplas requisições (conexões persistentes).
