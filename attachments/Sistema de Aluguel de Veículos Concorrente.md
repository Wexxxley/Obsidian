
O principal desafio em um sistema de aluguel de veículos é garantir que um veículo seja alugado por apenas um cliente de cada vez, especialmente quando há vários clientes tentando fazer reservas simultaneamente.

| Serviço                          | Responsabilidade                                                                                                                                                                                            |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Serviço de Frota (Servidor)**  | Gerencia o inventário de todos os  meios de transporte (Superclasse) e suas subclasses (carro, caminhão, ônibus, moto). É a única fonte de verdade sobre o _estado_ (Disponível, Reservado, Em Manutenção). |
| **Serviço de Locação (Cliente)** | Permite que o usuário/cliente interaja (faça reservas, cancele, registre devolução). Ele lida com as operações de Locação (Interface)5.                                                                     |

#### Verificação de Disponibilidade e Reserva
1. **Cliente:** O cliente solicita uma lista de veículos disponíveis e suas tarifas.
2. **Servidor:** O servidor consulta seu inventário e retorna os veículos com _status_ `Disponível`.
3. **Cliente:** O cliente seleciona um veículo e envia um **pedido de reserva** ao servidor.
4. **Servidor (Serviço de Frota):** O servidor deve:
    - **Bloquear (Lock) o Recurso:** Alocar o veículo logicamente para o cliente que fez o pedido.
    - **Atualizar o Estado:** Mudar o estado do veículo de `Disponível` para `Reservado`.
    - **Confirmar:** Enviar a confirmação da reserva de volta ao cliente.

Se **dois clientes** tentarem reservar o _mesmo_ **carro de passeio** ao mesmo tempo, o Serviço de Frota (Servidor) deve aplicar um **controle de concorrência**  para garantir que apenas um receba a confirmação e o estado seja atualizado de forma consistente. 

#### Registro de Multa Remoto 
1. **Cliente (Serviço de Locação):** Após a devolução, o cliente informa ao servidor sobre o estado do veículo. Se houver multas de trânsito, ele envia um **registro de multa**.
2. **Servidor (Serviço de Frota):** O servidor aplica a lógica da Interface **Multa** e anexa essa informação ao registro da locação.


---

### Por que isso é mais que CRUD

- **Controle de Concorrência:** O sistema precisa gerenciar acessos simultâneos ao recurso (o veículo) para evitar _overbooking_. Um CRUD simplesmente atualizaria o registro; um sistema distribuído precisa lidar com a **sincronização** de acesso à variável de estoque/status.
    
- **Transações Distribuídas:** A operação de reserva é uma transação que envolve a verificação do estado e a mudança do estado. Se a mudança de estado falhar (por um erro de rede ou falha no servidor), a transação inteira deve ser desfeita (_rollback_) para manter a **integridade dos dados**.
    
- **Tolerância a Falhas:** O Cliente deve ser programado para lidar com a **falha de comunicação**. O que acontece se o Serviço de Locação envia a reserva, mas não recebe a confirmação? O sistema pode usar mecanismos como _timeouts_ e **tentativas de comunicação (retries)** para garantir a entrega da mensagem.
    