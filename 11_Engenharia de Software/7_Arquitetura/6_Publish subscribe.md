
---
rão também visa construir sistemas distribuídos fracamente acoplados, mas com uma dinâmica de comunicação diferente das filas de mensagens ponto a ponto.

**Contexto:**

- Similar às filas, queremos desacoplar componentes em um sistema distribuído.
    
- No entanto, em vez de uma única entidade (produtor) enviando uma mensagem para outra entidade (consumidor) processar, queremos que uma entidade possa **anunciar um evento** sem saber quem (ou quantos) estão interessados nele.
    

**Conceito de Publish/Subscribe (Pub/Sub):**

- Baseia-se na ideia de **eventos** ou **tópicos**.
    
- Componentes podem assumir dois papéis principais (e às vezes ambos):
    
    - **Publicador (Publisher):** Anuncia (publica) mensagens sobre um determinado **tópico** ou evento para um intermediário (o _message broker_ ou _event bus_). O publicador não sabe quem vai receber a mensagem.
        
    - **Assinante (Subscriber):** Registra seu interesse (assina) em um ou mais **tópicos** junto ao intermediário. Quando uma mensagem é publicada em um tópico que ele assinou, o intermediário entrega a mensagem para ele.
        

**Componentes e Fluxo:**

1. **Publicador (Publisher):** Envia uma mensagem associada a um tópico específico para o intermediário.
    
2. **Intermediário (Message Broker / Event Bus):** Recebe as mensagens dos publicadores e as direciona para todos os assinantes que registraram interesse naquele tópico.
    
3. **Assinante (Subscriber):** Recebe as mensagens dos tópicos que assinou, enviadas pelo intermediário.
    

**Diferença Chave da Fila de Mensagens:**

- **Fila de Mensagens (Ponto a Ponto):** Geralmente, uma mensagem colocada na fila é consumida por **um único consumidor**. Mesmo que haja múltiplos consumidores para escalar o processamento, eles competem pela mensagem; apenas um a processará.
    
- **Publish/Subscribe (Um para Muitos):** Uma mensagem publicada em um tópico é entregue a **todos os assinantes** daquele tópico. Permite uma comunicação do tipo _broadcast_ para os interessados.
    

**Características Principais:**

- **Desacoplamento Extremo:** Publicadores e assinantes são completamente independentes. Eles não precisam se conhecer, nem saber quantos existem do outro lado. Só precisam conhecer o intermediário e os tópicos.
    
- **Comunicação Orientada a Eventos:** O fluxo é impulsionado pela ocorrência de eventos (mensagens publicadas).
    
- **Assíncrono:** A comunicação é inerentemente assíncrona.
    

**Benefícios:**

- **Alta Escalabilidade e Flexibilidade:** É fácil adicionar novos publicadores ou assinantes sem impactar os componentes existentes.
    
- **Desacoplamento Forte:** Maior independência entre os componentes do sistema.
    
- **Comunicação Um-para-Muitos Eficiente:** Ideal para cenários onde múltiplos componentes precisam reagir ao mesmo evento.
    

**Exemplos de Uso:**

- Notificação de eventos em tempo real (ex: atualização de status de um pedido para múltiplos sistemas: painel do cliente, sistema de logística, sistema de notificações).
    
- Sistemas de recomendação que reagem a ações do usuário (ex: um clique em um produto é publicado, e múltiplos motores de recomendação assinam esse tópico para atualizar suas sugestões).
    
- Atualização de caches em múltiplos servidores.
    

**Tecnologias Comuns:**

- Apache Kafka (muito usado para Pub/Sub em larga escala), RabbitMQ (também suporta Pub/Sub via _exchanges_), ActiveMQ, Google Cloud Pub/Sub, Amazon SNS.
    

Cobrimos o padrão Publish/Subscribe. Digite "next" para passarmos para outros padrões arquiteturais mencionados brevemente no livro.