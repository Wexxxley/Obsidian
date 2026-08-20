

---

### **1. Pagamento com Retenção em Custódia**

- **Estados da Transação:** O banco de dados precisará gerenciar um ciclo de vida para os pedidos (ex: `CRIADO`, `PAGO_RETIDO`, `EM_ANDAMENTO`, `CONCLUIDO_LIBERADO`, `ESTORNADO`).
    
- **Rotinas de Webhooks e Resiliência:** A plataforma deve implementar endpoints para escutar eventos assíncronos enviados pelo gateway (confirmação de pagamento, falhas de repasse e liquidações), garantindo que o status no banco de dados esteja sempre sincronizado.
    
- **Tratamento de Exceções e Mediação:** O módulo de Backoffice precisará de ferramentas para desbloqueio manual ou estorno caso ocorra uma contestação ou disputa entre o tutor e o cuidador.
### 2. Responsabilidade legal do cuidador 

No ordenamento jurídico brasileiro, ao receber o animal, o cuidador e o tutor firmam um "Contrato de Depósito". A plataforma atua apenas como intermediadora de tecnologia e pagamentos. Ao assumir a posse do animal, o cuidador torna-se o guardião temporário, assumindo a responsabilidade civil e criminal por danos, fugas ou negligência, enquanto o tutor mantém a responsabilidade por condições de saúde naturais e preexistentes.

**1. Formalização da Responsabilidade Legal no Software**
- **Termo de Guarda Temporária digital:** Deve haver uma etapa de aceite explícito de um Termo de Responsabilidade. O sistema precisa registrar o evento de aceite no banco de dados, gravando o timestamp, o endereço IP do usuário e a versão específica do documento.
- **Isenção Médica Específica:** O contrato digital embutido no sistema deve deixar claro que custos com doenças naturais ou genéticas são de responsabilidade do tutor. 

**2. Protocolo para Emergências Veterinárias (Doenças Naturais)**
- Durante a estadia, o cuidador precisa ter acesso rápido aos dados de saúde do pet. O sistema deve congelar as informações da ficha clínica no momento do check-in, impedindo mudanças.
- O cuidador deve agir com diligência (prestar socorro). O aplicativo deve possuir um "Botão de SOS" na tela da reserva ativa. Ao acionar essa rota na API, o sistema altera o status da reserva para alerta, dispara notificações _Push_ de alta prioridade para o tutor e registra no banco de dados que o cuidador cumpriu seu dever de informar imediatamente.
- Caso o cuidador precise pagar um atendimento de urgência do próprio bolso, o sistema deve permitir o anexo de notas fiscais veterinárias dentro do histórico da estadia para que o tutor realize o reembolso, mediado pelo módulo de Backoffice.
### 3. Fuga, Maus-Tratos ou Apropriação Indébita
- Como o cuidador assume a responsabilidade civil e criminal, a plataforma não pode permitir perfis não verificados. A arquitetura de software deve exigir o envio de frente e verso do RG/CNH e uma foto do rosto. O sistema valida essas informações (manualmente no Backoffice ou via APIs de terceiros) antes de mudar o status do usuário para `APROVADO`.      
- O sistema deve armazenar as fotos, as mensagens do chat e os registros de horários de forma estruturada. Se o cuidador alegar que o cachorro fugiu por acidente, a frequência das atualizações e as imagens do portão/casa servirão como prova para determinar se houve negligência.
- Em caso de denúncia de fuga, roubo ou agressão, o sistema aciona automaticamente o bloqueio dos valores. O montante pago pelo tutor permanece retido na subconta do gateway de pagamento, impedindo que o cuidador receba o lucro do serviço até que a investigação seja encerrada.