

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
- Classe responsável por gerenciar o estado dos usuários conectados ao servidor.
