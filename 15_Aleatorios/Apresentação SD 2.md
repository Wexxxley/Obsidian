


---
### 1. O Conceito de Push vs. Polling

**Servidor Antigo (Socket):**
- O servidor mantinha uma conexão de socket aberta com cada cliente.
- Quando "Ana" convidava "Bruno", o servidor simplesmente usava a conexão de Bruno e avisava que a ana tinha convidado.
- Isso é chamado de **Push**: o servidor pode empurrar uma notificação.
        
**Servidor Novo (RMI):** 
- O servidor RMI é stateless. O cliente faz uma chamada RMI, o servidor atende, responde e _desliga_. O servidor não pode ligar de volta para o cliente.
- Então, quando "Ana" convida "Bruno", o servidor vai até a fila/lista no `state_manager` de Bruno e "enfileira" um novo evento.
- O cliente de "Bruno", por sua vez, foi programado (no `main_html.js`) para checar sua fila a cada 2 segundos. Isso é o `setInterval` que chama `rmi_get_updates(token)`.
- Esse processo de checagem é chamado de **Polling**.     

---

#### 1. `send_request(...)`

- **O que faz:** O usuário "A" (requester) envia um pedido de amizade para o usuário "B" (target).
    
- **Ação de Enfileirar:** O servidor precisa notificar "B" de que ele tem um novo pedido.
    
- **Quem Recebe a Fila:** `target_nickname` (usuário "B").
    
- **O que é Enfileirado:** `{'command': 'INCOMING_FRIEND_REQUEST', 'from_nickname': 'A'}`
    
- **Resultado:** Na próxima vez que o cliente de "B" fizer o _polling_ (chamar `get_updates`), ele receberá esse evento e mostrará o `confirm()`: "Usuário 'A' quer te adicionar. Aceita?"
    

#### 2. `accept_request(...)`

- **O que faz:** O usuário "B" (acceptor) aceita o pedido de amizade do usuário "A" (requester).
    
- **Ação de Enfileirar:** O servidor precisa notificar **ambos** os usuários de que a amizade foi aceita.
    
- **Quem Recebe a Fila:** `requester_nickname` (usuário "A") **E** `acceptor_nickname` (usuário "B").
    
- **O que é Enfileirado (para "A"):** `{'command': 'FRIEND_REQUEST_ACCEPTED', 'by_nickname': 'B', 'status': ...}`
    
- **O que é Enfileirado (para "B"):** `{'command': 'FRIEND_REQUEST_ACCEPTED', 'by_nickname': 'A', 'status': ...}`
    
- **Resultado:** Ambos os clientes, em seu próximo _polling_, receberão este evento e adicionarão um ao outro em suas listas de contatos (e removerão o pedido pendente).
    

#### 3. `broadcast_status_update(...)`

- **O que faz:** O usuário "A" (`changed_user_nickname`) acabou de logar ou entrar em uma chamada. Seu status (`new_status_str`) mudou.
    
- **Ação de Enfileirar:** O servidor precisa notificar **todos os amigos** de "A" sobre essa mudança.
    
- **Quem Recebe a Fila:** O método primeiro busca a lista de amigos de "A" no banco (ex: "B", "C", "D"). Em seguida, ele enfileira o evento para cada um deles.
    
- **O que é Enfileirado (para "B", "C", "D"...):** `{'command': 'STATUS_UPDATE', 'nickname': 'A', 'status': 'Online'}`
    
- **Resultado:** Todos os amigos de "A", em seu próximo _polling_, receberão esse evento e atualizarão o indicador de status (a "bolinha" verde/cinza) ao lado do nome de "A" em suas listas de contato.