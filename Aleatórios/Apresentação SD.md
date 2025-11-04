

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
- ![](attachments/Pasted%20image%2020251104131321.png)
    - O método `create_message` implementa esse _framing_. Ele recebe um `command_code` e um dicionário `payload`, chama o método `serialize_payload` (que deve ser implementado pela subclasse) para obter os `payload_bytes`, e então constrói e retorna a mensagem completa: `header + payload_bytes`.
        

- Ele fornece implementações para serializar e desserializar tipos de dados comuns, como strings e listas de strings.
- ![](attachments/Pasted%20image%2020251104132110.png)
- 

---

### `VoipProtocol` (A Subclasse Concreta)

O `VoipProtocol` é a **implementação concreta** que herda do `BaseProtocol` (`class VoipProtocol(BaseProtocol):`). Ele implementa a lógica de negócios específica da aplicação VoIP, aderindo ao contrato definido pela classe base.

**Funções Técnicas:**

1. **Implementação do Contrato:**
    
    - Ele fornece as implementações concretas para `serialize_payload` e `deserialize_payload`, que estavam faltando na classe base.
        
2. **Lógica de _Dispatching_ (Despacho):**
    
    - **`serialize_payload`**: Contém um grande bloco `if/elif` que atua como um _dispatcher_ (despachante) baseado no `command_code`. Para cada `CommandCode`, ele sabe exatamente quais chaves esperar do dicionário `payload` (ex: para `LOGIN`, espera 'nickname' e 'password') e em que ordem serializá-las. Ele utiliza os métodos herdados (como `self.serialize_string`) para realizar a serialização.
        
    - **`deserialize_payload`**: É o _dispatcher_ inverso. Baseado no `command_code`, ele lê o `payload_bytes` na ordem exata em que foi escrito, usando `self.deserialize_string` e `struct.unpack_from` para reconstruir o dicionário `payload`.
        
3. **Definição do Protocolo de Aplicação:**
    
    - É esta classe que efetivamente define o protocolo de aplicação. A ordem e os tipos de dados em `serialize_payload` e `deserialize_payload` _são_ a especificação do protocolo. Qualquer cliente que queira se comunicar com o servidor deve aderir exatamente a essa ordem e formato de bytes para cada comando.
        

---

### Por que usar Herança? (Benefícios Técnicos)

1. **Reutilização de Código (DRY - Don't Repeat Yourself):** O `VoipProtocol` não precisa reescrever a lógica de _framing_ de mensagens (Header + Payload) ou a lógica complexa de serialização de strings com prefixo de comprimento. Ele herda essa funcionalidade testada e encapsulada do `BaseProtocol`.
    
2. **Separação de Responsabilidades (Separation of Concerns):**
    
    - `BaseProtocol` tem uma responsabilidade: a **estrutura** da mensagem e a **serialização de tipos primitivos** (como strings são delimitadas na rede).
        
    - `VoipProtocol` tem outra responsabilidade: o **conteúdo** da mensagem (a lógica de aplicação, como "o que constitui um comando `LOGIN`?").
        
    - Isso torna o código mais fácil de manter. Se você decidir mudar como as strings são serializadas (ex: usar 4 bytes para o comprimento), você só precisa mudar o `BaseProtocol`.
        
3. **Polimorfismo e Extensibilidade:** O resto do sistema, como o `client_handler.py`, interage com a instância `protocol` (que é do tipo `VoipProtocol`) através da interface definida pelo `BaseProtocol`. O `client_handler` chama `protocol.create_message` e `protocol.deserialize_payload`. Ele não precisa saber os detalhes internos do `VoipProtocol`, apenas que ele cumpre o contrato do `BaseProtocol`. Se, no futuro, você quisesse criar um `AdminProtocol(BaseProtocol)` com comandos diferentes, o `client_handler` poderia, teoricamente, lidar com ambos contanto que eles respeitem a mesma interface base.