
Este sistema separa as responsabilidades da Locadora em dois serviços rodando em computadores separados: o **Serviço de Frota (Servidor)**, que gerencia o estado dos recursos, e o **Serviço de Locação (Cliente)**, que interage com o usuário. A comunicação será mista, utilizando chamadas **síncronas** para operações de tempo real e **assíncronas** para tarefas em segundo plano.

| Serviço                          | Responsabilidade                                                                                                                       |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| **Serviço de Frota (Servidor)**  | Única fonte de verdade sobre o **inventário** (cadastro) e o **estado** (Disponível, Reservado, Em Manutenção) de todos os veículos.   |
| **Serviço de Locação (Cliente)** | Lida com a interface do usuário, enviando **requisições síncronas** para reserva e **mensagens assíncronas** para tarefas secundárias. |
### Comunicação Síncrona
As operações que exigem uma resposta imediata e manipulam o estado crítico do recurso devem usar a comunicação síncrona para garantir que o cliente saiba imediatamente o resultado.

1. **Cliente:** Solicita uma lista de veículos disponíveis.
2. **Servidor:** Retorna os veículos com _status_ Disponível.
3. **Cliente:** Seleciona um veículo e envia um **pedido de reserva** (chamada síncrona).
4. **Servidor:**
    - O Servidor aplica o **Controle de Concorrência** para o veículo específico.
    - **Atualiza o Estado:** Se o bloqueio for bem-sucedido, muda o estado de Disponível para Reservado.
    - **Confirma:** Envia a confirmação da reserva (resposta síncrona) de volta ao Cliente.

O uso síncrono é essencial para garantir a **Atomicidade** da transação e evitar o _overbooking_ quando múltiplos clientes acessam o mesmo recurso simultaneamente.
### Comunicação Assíncrona
Tarefas que podem ser processadas em segundo plano, sem bloquear o usuário, devem utilizar um modelo de **Mensageria Assíncrona** (Filas de Mensagens) para **desacoplar** os serviços.

#### Fluxo Assíncrono para Registro de Multa e Processamento de Devolução

1. **Cliente (Serviço de Locação):**
    
    - Após a devolução do veículo, o Cliente finaliza o processo para o usuário.
        
    - Se houver uma multa, o Cliente **envia uma mensagem durável** contendo os dados do veículo e da multa para a **Fila de Multas**.
        
    - O Cliente não espera por uma resposta e continua sua execução.
        
2. **Fila de Mensagens:**
    
    - A mensagem da multa fica armazenada na fila. **Tolerância a Falhas:** Se o Servidor de Frota estiver fora do ar, a mensagem é garantida e não é perdida.
        
3. **Servidor (Serviço de Frota):**
    
    - O Servidor funciona como um **Consumidor** que monitora e processa mensagens da Fila de Multas.
        
    - Ao consumir a mensagem, ele aplica a lógica da Interface **Multa** e anexa essa informação ao registro da locação.
        
    - Após o processamento, ele pode enviar outra mensagem assíncrona (ex: para uma Fila de Notificações) para enviar um recibo por e-mail ao cliente.
        
