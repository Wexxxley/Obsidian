

---

Um **protocolo de requisição-resposta** é projetado especificamente para suportar a troca de mensagens típica entre um cliente e um servidor.

- Normalmente, a comunicação é **síncrona**: o cliente envia uma requisição e fica bloqueado esperando a resposta do servidor.

- Pode ser projetado para ser **confiável**, pois a resposta do servidor serve como uma confirmação implícita de que a requisição foi recebida.

---
### **1. Primitivas de Comunicação**

1. **doOperation**: Usada pelo cliente para invocar uma operação remota. Envia a mensagem de requisição e bloqueia esperando a mensagem de resposta. 
    
2. **getRequest**: Usada pelo servidor para receber uma mensagem de requisição de um cliente.
    
3. **sendReply**: Usada pelo servidor para enviar a mensagem de resposta de volta ao cliente que fez a requisição.
    
![](attachments/Pasted%20image%2020251029105559.png)

1. **Cliente:** Monta uma mensagem contendo a operação desejada e os dados necessários. 
2. **Cliente:** Envia essa mensagem pela rede para o endereço do servidor (IP e porta).
3. **Cliente:** Entra em estado de espera (bloqueio).
4. **Servidor:** Está em um "loop de escuta". Ao receber a mensagem, ele a interpreta.
5. **Servidor:** Executa a ação solicitada.
6. **Servidor:** Monta uma mensagem de resposta contendo o resultado.
7. **Servidor:** Envia a resposta de volta ao cliente.
8. **Cliente:** Recebe a resposta, "desbloqueia" e continua sua execução.

---
### **2. Estrutura da Mensagem**

- **Tipo de Mensagem**: Request ou Resposta.
- **ID da Requisição**: Um identificador único gerado pelo cliente para cada requisição. O servidor copia esse ID na resposta correspondente, permitindo que o cliente associe a resposta à requisição correta e descarte respostas de requisições antigas ou duplicadas.
- **Referência Remota**: Identifica o objeto ou serviço remoto sendo invocado.
- **ID da Operação**: Identifica qual operação específica deve ser executada.
    
![](attachments/Pasted%20image%2020251029105832.png)

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
