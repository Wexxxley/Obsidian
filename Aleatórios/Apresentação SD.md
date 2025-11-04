

---
### 1. Apresentação da estrutura da aplicação (kauan)

Nosso projeto é um sistema de comunicação voice ip...
Mostrar as imagens e explicar...

---
### 2. Mostrar que os conceitos principais de poo foram atendidos (wesley)

![](attachments/Pasted%20image%2020251104125618.png)

- Utilizamos 3 linguagens diferentes: 
	- c++ para o server de relay por seu auto desempenho uma vez que ele vai precisar enviar os fluxos de audio dos clientes.
	- Python para o servidor de sinalização. Servidor esse responsável por conectar os clientes e tratar tudo que não for a ligação em sí.
	- Utilizamos Electron para a interface do cliente, permitindo o uso de node, html e css.

#### Protocol
- O `BaseProtocol` é uma **Superclasse Abstrata**. Sua principal função é fornecer métodos de serialização reutilizáveis para qualquer protocolo binário.
- O `BaseProtocol` define o formato de cabeçalho que todas as mensagens devem seguir:1 byte para o CommandCode e 2 bytes para o tamanho do payload subsequente.
- O método `create_message` recebe um `command_code` e um dicionário `payload`, chama o método `serialize_payload` (que deve ser implementado pela subclasse) e então constrói e retorna a mensagem completa: `header + payload_bytes`.
- ![](attachments/Pasted%20image%2020251104132554.png)
- Ele fornece implementações para serializar e desserializar tipos de dados comuns, como strings e listas de strings.
- ![](attachments/Pasted%20image%2020251104132110.png)
- O `VoipProtocol` é a **implementação concreta**. Ele implementa a lógica de negócios específica da aplicação VoIP.
    - **`serialize_payload`**: Contém um grande bloco `if/elif` que atua como um despachante. Para cada `CommandCode`, ele sabe exatamente quais chaves esperar do dicionário `payload` e em que ordem serializá-las. 
        
    - **`deserialize_payload`**: É o despachante inverso. Baseado no `command_code`, ele lê o `payload_bytes` na ordem exata em que foi escrito para reconstruir o dicionário `payload`.
        
#### StateManager
- É o gerenciador de estado  e thread-safe do servidor.
- Sua principal responsabilidade é manter um dicionário (`_connected_users`) que mapeia o `nickname` de um usuário ao seu objeto `ConnectedUser`.
- A parte mais importante é o `_lock = threading.Lock()`. Como o seu servidor usa threads (uma para cada cliente), várias threads podem tentar adicionar ou remover usuários ao mesmo tempo. O `_lock`garante que apenas **uma thread por vez** possa acessar

#### Interfaces e serviços
- Definimos algumas interfaces para serviços.
- Como por exemplo **AuthenticationService** que implementa a lógica de  `login_user` e `Register_user
- Da mesma forma, `CallService` implementa `create_call_session` que cria uma sessão com um token identificador da sessao que é enviado para ambos os participantes.

#### Classes pojos
Algumas classes pojos foram criadas como: 
- ConnectedUser, que representa um user conectado
- Friendship
- UserProfile
- ServerResponse

---
### 3. Apresentação simplificada do serve de sinalização

**Server**
- Quando o cliente se conecta é o arquivo server que vai fazer o primeiro contato e então encaminhar para client_dandler através de outra thread.
- O server fica em espera com a a thread principal

**Client_handler**
- Gerencia o ciclo de vida da conexão de um _único_ cliente, rodando em sua própria thread. 

- Fica em um loop aguardando dados especificamente daquele cliente.

- Ele é responsável por ler os bytes da rede de forma estruturada: primeiro lê o cabeçalho (3 bytes), depois usa o tamanho lido do cabeçalho para ler o restante (o payload).    

- Utiliza o `protocol.deserialize_payload` para traduzir os bytes brutos do payload em um dicionário Python que o servidor possa entender.
    
- Porém client handler NÃO sabe como funciona comandos; ele apenas encaminha o comando e o dicionário para o `command_router.route_command`.
    
- Quando o cliente desconecta,  o bloco `finally` é executado para limpar o estado: remove o usuário do `state_manager` e avisa os amigos que ele ficou 'Offline'.

**Command_router**
- Ele recebe o comando e o payload do `client_handler`.
    
- Usa o `COMMAND_MAP` para mapear o `CommandCode` (ex: `LOGIN`) para a função de tratamento correta (ex: `handle_login`).
    
- Orquestra a execução da lógica de negócios, chamando os `services` (ex: `auth_service.login_user`) e o `state_manager`.
    
- Envia respostas de volta ao cliente usando as funções do `client_handler` (ex: `send_binary_message`).    

**Db_manager**

- É a camada de acesso a dados (Data Access Layer - DAL) do aplicativo.
    
- Contém todas as funções que executam consultas SQL diretamente no banco de dados (ex: `INSERT`, `SELECT`, `UPDATE`).
    
- Funções como `register_user` e `check_login` lidam com a lógica de banco de dados para usuários, incluindo _hashing_ de senhas.
    
- Funções como `add_friend_request_db` e `get_friends_list_db` gerenciam a lógica de amizades no banco de dados.
    
- É chamado pelos `services` para persistir ou recuperar dados.
    

**Interfaces**

- Define "contratos" formais usando Classes Base Abstratas (ABC).
    
- Dita _quais_ métodos os serviços _devem_ implementar, mas não _como_ eles fazem isso (ex: `IAuthenticationService` exige um método `login_user`).
    
- Serve para garantir a consistência da arquitetura e permitir a inversão de dependência (embora não esteja totalmente explorada no projeto, ela define a estrutura para isso).
    

**Protocol**

- Define o "idioma" binário exato que o cliente e o servidor usam para se comunicar.
    
- Lista todos os `CommandCode` (os "verbos" da comunicação, ex: `LOGIN`, `INVITE`) em um `IntEnum`.
    
- Contém a classe `VoipProtocol` que herda do `BaseProtocol`, e é responsável por serializar (Python dict -> bytes) e desserializar (bytes -> Python dict) os payloads de cada comando.
    

**Services**

- Contém a **lógica de negócios** (regras de aplicação) do servidor.
    
- Atua como um intermediário entre o `command_router` e o `db_manager`/`state_manager`.
    
- `AuthenticationService`: Lida com as regras de registro e login (ex: verifica se o usuário já está online no `state_manager` _após_ verificar as credenciais no `db_manager`).
    
- `FriendshipService`: Gerencia a lógica de amizades (ex: buscar amigos e, em seguida, obter seu status online do `state_manager`).
    
- `CallService`: Lida com a lógica de chamadas (ex: gerar tokens de sessão e obter as informações do Relay do `config`).