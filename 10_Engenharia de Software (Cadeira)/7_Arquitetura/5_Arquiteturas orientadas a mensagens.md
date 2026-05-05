
#Concluded 

---

Em sistemas distribuídos, a comunicação direta entre serviços pode criar acoplamento temporal e de disponibilidade. 
- Se o serviço B estiver indisponível quando o serviço A tentar chamá-lo, a operação em A falhará.  
- Além disso, picos de carga em um serviço podem sobrecarregar outros serviços que dependem dele diretamente.    

---
### **1. Fila de mensagens**

Para resolver esses problemas, introduz-se um componente intermediário: uma **fila de mensagens**. Em vez de se comunicarem diretamente, os serviços se comunicam através dessa fila.

**Fluxo:**
1. **Produtor:** Um serviço que precisa enviar uma informação ou solicitar que uma tarefa seja realizada por outro serviço. Ele não envia a requisição diretamente ao destinatário, mas sim **publica uma mensagem** na fila.
2. **Fila de Mensagens:** Um repositório intermediário que armazena as mensagens enviadas pelos produtores de forma ordenada. Ela desacopla o produtor do consumidor.
3. **Consumidor:** Um serviço que está interessado nas mensagens de uma determinada fila. Ele **recupera as mensagens** da fila e as processa no seu próprio ritmo.

![](../../attachments/Pasted%20image%2020251026162626.png)

---
### **Características Principais**

- **Comunicação Assíncrona:** O produtor publica a mensagem e não precisa esperar que o consumidor a processe. Ele pode seguir com suas outras tarefas. O consumidor processa a mensagem quando puder.
- **Desacoplamento:** O produtor não precisa conhecer o consumidor e vice-versa. Eles só precisam conhecer a fila. Isso reduz as dependências diretas entre os serviços.
- **Persistência (Opcional):** Muitas filas de mensagens oferecem persistência, garantindo que as mensagens não sejam perdidas mesmo que o consumidor esteja temporariamente indisponível ou que o sistema de filas falhe.    
- **Maior Resiliência/Disponibilidade:** Se o consumidor estiver temporariamente offline, as mensagens se acumulam na fila e serão processadas quando ele voltar. 
- **Balanceamento de Carga:** Se houver um pico de mensagens enviadas pelo produtor, a fila age como um _buffer_. Os consumidores podem processar as mensagens em um ritmo mais constante, evitando sobrecarga.
- **Escalabilidade:** É fácil escalar produtores e consumidores de forma independente. Se o processamento das mensagens estiver lento, basta adicionar mais instâncias do serviço consumidor lendo da mesma fila.
- **Desacoplamento Temporal e Lógico:** Produtores e consumidores não precisam estar ativos ao mesmo tempo e não precisam conhecer detalhes uns dos outros.
    
**Exemplos de Uso:**
- Processamento de pedidos em e-commerce (o serviço de front-end publica um pedido na fila, e serviços de back-end de estoque, pagamento, envio consomem a mensagem).
- Processamento de tarefas em background que podem levar mais tempo.