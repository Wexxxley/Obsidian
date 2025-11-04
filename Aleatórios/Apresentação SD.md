

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
        
    - Da mesma forma, `CallService` implementa `create_call_session` usando o módulo `secrets` e as variáveis do `config`.
        

---

### 💡 Por que usar Interfaces? (O Benefício)

Usar interfaces (abstrações) em vez de depender diretamente das classes concretas (serviços) é um pilar da arquitetura de software, e os benefícios são enormes:

1. **Testabilidade (Mocking)**
    
    - **Problema:** Como você testa o `command_router.py` (que lida com um login) sem precisar de um banco de dados real e do `state_manager` online?
        
    - **Solução:** Nos seus testes, você pode criar uma classe "falsa" chamada `MockAuthenticationService(IAuthenticationService)`. Como ela implementa a mesma interface, ela terá os métodos `register_user` e `login_user`. Você pode programar o `login_user` falso para simplesmente retornar `(True, "Login OK")` sem tocar em nenhum banco de dados.
        
    - Isso permite que você teste a lógica do `command_router` de forma **isolada**, o que é a base dos testes unitários eficazes.
        
2. **Desacoplamento (Princípio da Inversão de Dependência)**
    
    - Isso significa que módulos de alto nível (como o `command_router.py`) não devem depender de detalhes de baixo nível (como o `db_manager.py` ou o `state_manager`). Ambos devem depender de **abstrações** (`interfaces.py`).
        
    
    - **Exemplo Prático:** Imagine que você queira trocar seu `AuthenticationService` (que usa SQLite) por um novo `RedisAuthService` (que valida tokens em um cache Redis).
        
    - Contanto que o seu novo `RedisAuthService` **implemente a interface `IAuthenticationService`**, o seu `command_router` não precisará de **nenhuma modificação**. Ele continuará chamando `auth_service.login_user(...)`, e não fará ideia (nem precisa saber) que a lógica por trás foi completamente substituída.
        
3. **Clareza e Contrato de API**
    
    - O arquivo `interfaces.py` age como uma documentação de alto nível. Um novo desenvolvedor pode ler _apenas_ esse arquivo e entender rapidamente _todas as capacidades_ do seu sistema (`register_user`, `send_request`, `create_call_session`, etc.) sem precisar se perder nos detalhes da implementação.
        

Em resumo, as **interfaces** definem o "o quê" (API), e os **serviços** definem o "como" (lógica). Usar essa separação torna seu código