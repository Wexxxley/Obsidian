
#Concluded 

---
Similar às filas, queremos desacoplar componentes em um sistema distribuído. No entanto, em vez de uma única entidade (produtor) enviando uma mensagem para outra entidade (consumidor) processar, queremos que uma entidade possa **anunciar um evento** sem saber quem (ou quantos) estão interessados nele. Baseia-se na ideia de **eventos** ou **tópicos**.

- **Publicador:** Anuncia mensagens sobre um determinado **tópico** ou evento para um intermediário. O publicador não sabe quem vai receber a mensagem.
- **Assinante:** Registra seu interesse em um ou mais **tópicos** junto ao intermediário. Quando uma mensagem é publicada em um tópico que ele assinou, o intermediário entrega a mensagem para ele.

![](../../../attachments/Pasted%20image%2020251026174022.png)

**Componentes e Fluxo:**
1. **Publicador:** Envia uma mensagem associada a um tópico específico para o intermediário.
2. **Intermediário:** Recebe as mensagens dos publicadores e as direciona para todos os assinantes que registraram interesse naquele tópico.
3. **Assinante:** Recebe as mensagens dos tópicos que assinou, enviadas pelo intermediário.

**Características Principais:**
- **Desacoplamento Extremo:** Publicadores e assinantes são completamente independentes. Eles não precisam se conhecer, nem saber quantos existem do outro lado. Só precisam conhecer o intermediário e os tópicos.
- **Comunicação Orientada a Eventos:** O fluxo é impulsionado pela ocorrência de eventos 
- **Assíncrono:** A comunicação é inerentemente assíncrona.
- **Alta Escalabilidade e Flexibilidade:** É fácil adicionar novos publicadores ou assinantes sem impactar os componentes existentes.
- **Comunicação Um-para-Muitos Eficiente:** Ideal para cenários onde múltiplos componentes precisam reagir ao mesmo evento.

**Exemplos de Uso:**
- Notificação de eventos em tempo real (ex: atualização de status de um pedido para múltiplos sistemas: painel do cliente, sistema de logística, sistema de notificações).
- Sistemas de recomendação que reagem a ações do usuário (ex: um clique em um produto é publicado, e múltiplos motores de recomendação assinam esse tópico para atualizar suas sugestões).
