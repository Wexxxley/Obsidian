
___

Sistema de Aluguel de Veículos Concorrente

O principal desafio em um sistema de aluguel de veículos é garantir que um veículo seja alugado por apenas um cliente de cada vez, especialmente quando há vários clientes tentando fazer reservas simultaneamente.

### 1. Separação Funcional Mais Clara

Vamos renomear os serviços para refletir suas responsabilidades de forma mais precisa, baseadas nas classes e interfaces sugeridas1:

|Serviço|Responsabilidade (Servidor)|Conceitos de POO 2|
|---|---|---|
|**Serviço de Frota e Status (Servidor)**|Gerencia o inventário (cadastro) de todos os **Meios de Transporte** (Superclasse) e suas subclasses (**carro de passeio, caminhão, ônibus, moto, etc.**)3. É a única fonte de verdade sobre o _estado_ (`Disponível`, `Reservado`, `Em Manutenção`).||**Superclasse/Subclasses**, **Agregação** (a Locadora possui os veículos)4.|
|**Serviço de Locação e Cliente (Cliente)**|Permite que o usuário/cliente interaja (faça reservas, cancele, registre devolução). Ele lida com as operações de **Locação** (Interface)5.||**Interface** (Locação, Multa)6.|

### 2. Fluxos de Comunicação Críticos e Concorrência

Para justificar o sistema distribuído, foque nestes fluxos remotos:

#### A. Verificação de Disponibilidade e Reserva (O Desafio Central)

1. **Cliente (Serviço de Locação):** O cliente solicita uma lista de veículos disponíveis e suas tarifas.
    
2. **Servidor (Serviço de Frota):** O servidor consulta seu inventário e retorna os veículos com _status_ `Disponível`.
    
3. **Cliente (Serviço de Locação):** O cliente seleciona um veículo e envia um **pedido de reserva** ao servidor.
    
4. **Servidor (Serviço de Frota):** Esta é a etapa crítica. O servidor deve:
    
    - **Bloquear (Lock) o Recurso:** Alocar o veículo logicamente para o cliente que fez o pedido.
        
    - **Atualizar o Estado:** Mudar o estado do veículo de `Disponível` para `Reservado`.
        
    - **Confirmar:** Enviar a confirmação da reserva de volta ao cliente.
        

**O Conceito Distribuído:** Se **dois clientes** tentarem reservar o _mesmo_ **carro de passeio** ao mesmo tempo, o Serviço de Frota (Servidor) deve aplicar um **controle de concorrência** (ex: um _lock_ ou um sistema de filas) para garantir que apenas um receba a confirmação e o estado seja atualizado de forma consistente. Isso vai muito além do CRUD.

#### B. Registro de Multa Remoto (Interfaces Distribuídas)

1. **Cliente (Serviço de Locação):** Após a devolução, o cliente informa ao servidor sobre o estado do veículo. Se houver multas de trânsito7, ele envia um **registro de multa**.
    
2. **Servidor (Serviço de Frota):** O servidor aplica a lógica da Interface **Multa** 8 e anexa essa informação ao registro da locação.
    

**O Conceito Distribuído:** O **Serviço de Frota** atua como um _Gateway_ que implementa as regras da interface **Multa**9, processando a informação recebida remotamente do **Serviço de Locação**.

---

### Por que isso é mais que CRUD

- **Controle de Concorrência:** O sistema precisa gerenciar acessos simultâneos ao recurso (o veículo) para evitar _overbooking_. Um CRUD simplesmente atualizaria o registro; um sistema distribuído precisa lidar com a **sincronização** de acesso à variável de estoque/status.
    
- **Transações Distribuídas:** A operação de reserva é uma transação que envolve a verificação do estado e a mudança do estado. Se a mudança de estado falhar (por um erro de rede ou falha no servidor), a transação inteira deve ser desfeita (_rollback_) para manter a **integridade dos dados**.
    
- **Tolerância a Falhas:** O Cliente deve ser programado para lidar com a **falha de comunicação**. O que acontece se o Serviço de Locação envia a reserva, mas não recebe a confirmação? O sistema pode usar mecanismos como _timeouts_ e **tentativas de comunicação (retries)** para garantir a entrega da mensagem.
    

Implementar a comunicação (ex: usando sockets, RPC ou Web Services) e o controle de concorrência no Servidor transformará este trabalho em um projeto de sistemas distribuídos significativo.