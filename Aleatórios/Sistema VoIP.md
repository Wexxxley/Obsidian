
---

# **1. ARQUITETURA**

---
#### Camada 1: Apresentação (Cliente)

**Componente**: Cliente VoIP Desktop.
**Linguagem:** C++. 
**Responsabilidades:**
- Apresentar a Interface do Utilizador (GUI).
- Gerir a interação do utilizador (login, ligar, desligar).
- Comunicar com a Camada de Lógica (Sinalização) via TCP.
- Enviar e receber o fluxo de áudio (UDP) para a Camada de Lógica (Media Relay).

---
#### Camada 2: Lógica (Backend)

**Componente 2a**: Servidor de Sinalização
**Linguagem Proposta:** Python. 
**Responsabilidades:**
- Gerir conexões TCP persistentes com os clientes.
- Orquestrar todo o ciclo de vida da chamada (INVITE, ACCEPT, BYE).
- Autenticar utilizadores, consultando a Camada de Dados.
- Manter o estado de cada utilizador (Disponível, Em Chamada, etc.).

**Componente 2b: Servidor de Mídia (Media Relay)**
**Linguagem**: C++. Esta é uma tarefa de alta performance. 
**Responsabilidades:**
- Receber pacotes UDP de um cliente.
- Identificar a sessão da chamada.
- Reencaminhar (fazer o "relay") o pacote para o outro cliente na sessão.

---
#### Camada 3: Dados

**Componente**: Banco de Dados Relacional.
**Tecnologia Proposta:** PostgreSQL (para um sistema robusto) ou SQLite (para simplicidade).
**Responsabilidades**:
- Armazenar de forma segura os dados dos utilizadores (nomes, senhas criptografadas). 
- Manter listas de contactos e outras informações persistentes. 
- Fornecer uma fonte de verdade para a autenticação realizada pela Camada de Lógica.

---

# **2. Requisitos Funcionais (RF)**

---

- **RF-01: Gestão de Contas de Utilizador**
    - `RF-01.1:` O sistema deve permitir que um novo utilizador se registe fornecendo as informações necessárias (Nickname, senha).
    - `RF-01.2:` O sistema deve garantir que cada nickname seja único.
        
- **RF-02: Autenticação de Utilizador**
    - `RF-02.1:` O utilizador registado deve fazer login (nickname e senha) para acessar.
        
- **RF-03: Gestão de Presença**
    - `RF-03.1:` O sistema deve manter e exibir o estado de presença dos utilizadores (ex: `Online`, `Offline`, `Em Chamada`).
    - `RF-03.2:` O sistema deve atualizar automaticamente o estado de um utilizador quando este se autentica (`Online`), inicia uma chamada (`Em Chamada`), termina uma chamada (`Online`) ou se desconecta (`Offline`).
        
- **RF-04: Gestão de Contactos**
    - `RF-04.1:` O sistema deve permitir que um utilizador visualize a lista dos seus contactos.
	- **`RF-04.2:`** O sistema deve permitir que um utilizador procure outros utilizadores registados no sistema (por nickname).
	- **`RF-04.3:`** O sistema deve permitir que um utilizador envie um pedido de adição de contacto a outro utilizador.    
	- **`RF-04.4:`** O sistema deve permitir que um utilizador aceite ou recuse um pedido de adição de contacto recebido.

- **RF-05: Comunicação por Voz**
    - `RF-05.1:` O sistema deve permitir que um utilizador inicie uma chamada de voz com outro utilizador que esteja com o estado `Online`.
    - `RF-05.2:` O sistema deve permitir que um utilizador receba e aceite ou recuse um convite para uma chamada de voz.
    - `RF-05.3:` O sistema deve permitir que qualquer um dos participantes encerre uma chamada de voz a qualquer momento.

---
# **3. Casos de Uso (UC)**

---

**UC-01: Registar Novo Utilizador**
- **Ator Principal:** Utilizador não registado.
- **Objetivo:** Criar uma nova conta no sistema.
- **Pré-condições:** O utilizador tem acesso ao cliente da aplicação.
- **Fluxo Principal:**
    1. O utilizador seleciona a opção de registo.
    2. O sistema apresenta um formulário para a inserção de dados (nome de utilizador, senha).
    3. O utilizador preenche e submete o formulário.
    4. O sistema valida os dados, cria o registo do novo utilizador e informa o sucesso da operação.
        
- **Fluxo de Exceção (Nome de utilizador já existe):**    
    1. No passo 4, se o nome de utilizador já existir, o sistema informa o erro ao utilizador, que pode então tentar um novo nome (retorna ao passo 3).

---
**UC-02: Autenticar Utilizador**
- **Ator Principal:** Utilizador registado.
- **Objetivo:** Aceder ao sistema de forma segura.
- **Pré-condições:** O utilizador possui uma conta válida.
- **Fluxo Principal:**
    1. O utilizador abre a aplicação.
    2. O sistema apresenta os campos para inserção de credenciais.
    3. O utilizador insere o seu nome de utilizador e senha e solicita o login.
    4. O sistema valida as credenciais, estabelece a sessão do utilizador, define seu estado para `Online` e apresenta a interface principal.
        
- **Fluxo de Exceção (Credenciais inválidas):**
    1. No passo 4, se as credenciais forem inválidas, o sistema informa o erro ao utilizador, que pode corrigir os dados e tentar novamente (retorna ao passo 3).

---
**UC-03: Realizar Chamada de Voz**
- **Atores:** Utilizador Chamador, Utilizador Chamado.
- **Objetivo:** Estabelecer um canal de comunicação de áudio entre dois utilizadores.
- **Pré-condições:** Ambos os utilizadores estão autenticados e com estado `Online`.
- **Fluxo Principal:**
    1. O Utilizador Chamador seleciona um contacto na sua lista e aciona a função "Ligar".
    2. O sistema envia um convite de chamada para o Utilizador Chamado.
    3. O sistema notifica o Utilizador Chamado sobre a chamada recebida, exibindo quem está a ligar e as opções de "Aceitar" ou "Recusar".
    4. O Utilizador Chamado seleciona "Aceitar".
    5. O sistema estabelece a conexão de mídia entre os dois clientes.
    6. O sistema atualiza o estado de ambos os utilizadores para `Em Chamada`.
    7. Os utilizadores conversam entre si.
    8. Um dos utilizadores (A ou B) seleciona "Desligar".
    9. O sistema encerra a sessão de mídia.
    10. O sistema atualiza o estado de ambos os utilizadores para `Online`.

- **Fluxos Alternativos:**
    - **Utilizador Chamado Recusa a Chamada:** No passo 4, se o Utilizador Chamado selecionar "Recusar", o sistema informa o Chamador da recusa e a chamada não é estabelecida.
        
---
**UC-04: Adicionar Novo Contacto**

- **Atores:** Utilizador Requisitante, Utilizador Convidado.
- **Objetivo:** Adicionar um novo utilizador à lista de contactos pessoal.
- **Pré-condições:**
    - O Utilizador Requisitante está autenticado no sistema.
    - O Utilizador Convidado possui uma conta válida no sistema.
        
- **Fluxo Principal:**
    1. O Utilizador Requisitante aciona a função para procurar e adicionar um novo contacto.
    2. O sistema apresenta uma interface de busca.
    3. O Requisitante insere o nome de utilizador do Convidado e inicia a busca.
    4. O sistema exibe o perfil do Utilizador Convidado encontrado.
    5. O Requisitante seleciona a opção "Adicionar Contacto".
    6. O sistema envia um pedido de contacto para o Utilizador Convidado.
    7. O sistema notifica o Utilizador Convidado sobre o novo pedido.
    8. O Utilizador Convidado visualiza o pedido pendente e seleciona "Aceitar".
    9. O sistema estabelece a ligação de contacto mútua:
        - Adiciona o Convidado à lista do Requisitante.
        - Adiciona o Requisitante à lista do Convidado.
        
- **Fluxos Alternativos:**
    - **Utilizador Não Encontrado:** No passo 4, se o nome de utilizador inserido não corresponder a nenhum registo, o sistema informa o Requisitante, que pode tentar uma nova busca (retorna ao passo 3).
    - **Pedido Recusado:** No passo 8, se o Utilizador Convidado selecionar "Recusar", o sistema cancela o pedido.
    - **Contacto Já Existente:** No passo 5, se os utilizadores já forem contactos, o sistema deve informar o Requisitante e impedir o envio de um novo pedido.

---

# 4. GUI

---

#### **1. Janela de Autenticação (Estado Inicial)**

Esta é a primeira coisa que o utilizador vê.  Uma única janela que pode alternar entre dois formulários.

- **Formulário de Login:**
    - `[Campo de Texto]` Nickname do utilizador.
    - `[Campo de Texto]` Senha (deve mascarar os caracteres).
    - `[Botão]` **Entrar**.
    - `[Link]` "Ainda não tem conta? Registe-se".
    - `[Área de Texto]` Para exibir mensagens de erro (ex: "Nickname ou senha inválidos")
        
- **Formulário de Registo:**    
    - `[Campo de Texto]` Nickname desejado.
    - `[Campo de Texto]` Senha.
    - `[Campo de Texto]` Confirmação da Senha.
    - `[Botão]` **Criar Conta**.
    - `[Link]` "Já tem uma conta? Faça o login".
    - `[Área de Texto]` Para exibir mensagens (ex: "Utilizador já existe")

---
#### **2. Janela Principal (Após Login)**

- **Informações do Utilizador Logado:**
    - `[Indicador Visual]` Mostrando o seu próprio status e nickname.
    - `[Botão]` **Logout/Sair**.
        
- **Lista de Contactos:**
    - Este é o componente principal. Deve ser uma lista rolável.
    - **Para cada item da lista de contactos:**
        - `[Indicador Visual de Status]` Um círculo colorido (ex: Verde para `Online`, Vermelho para `Em Chamada`, Cinza para `Offline`).
        - `[Label]` Nickname do contacto.
        - `[Botão]` **Ligar**. Este botão deve estar **desativado** se o status do contacto não for `Online`.
            
- **Gestão de Contatos:**
    - `[Botão]` **Adicionar Contacto**. Ao ser clicado, abre a janela de busca.

---
#### **3. Janelas adicionais**

Estas são janelas menores que aparecem sobre a janela principal para tarefas específicas.

- **Diálogo de Adicionar Contacto:**
    - `[Campo de Texto]` "Procurar por nickname...".
    - `[Botão]` **Procurar**.
    - `[Área de Resultados]`mostrando o utilizador encontrado com nickname e um botao `Enviar Pedido.
         
- **Chamada Recebida (Alerta):**
    - Este deve aparecer de forma proeminente na tela.
    - `[Label]` "**[Nickname do Chamador]** está a ligar...".
    - `[Botão]` **Aceitar**.
    - `[Botão]` **Recusar**.
        
- **Janela de Chamada:**
    - **Estado 1: A Ligar (Outgoing)**
        - `[Label]` "A ligar para **[Nickname do Chamado]**...".
            
    - **Estado 2: Em Chamada (Ativa)**
        - `[Label]` "Em chamada com **[Nome do Contacto]**".
        - `[Botão]` **Desligar**.


---

# **Classes POJO (Plain Old Java Objects)**

1. **`UserInfo`**: Representa os dados de um utilizador que são seguros para transitar pela rede (sem a senha).
    - **Atributos:**
        - `String nickname`
        - `String status` (ex: "Online", "Offline", "Em Chamada")
            
2. **`CallInvitation`**: Representa as informações de um convite de chamada.
    - **Atributos:**
        - `String callerNickname` (Nickname de quem está a ligar)
        - `String calleeNickname` (Nickname de quem está a receber)
        - `String callId` (Um identificador único para esta chamada)
            

#### **Classes de Modelo que Implementam Serviços**
Estas são as classes no backend que contêm a lógica de negócio e _efetivamente realizam_ o trabalho do serviço remoto. Vocês precisam de pelo menos duas. Uma boa prática é separar as responsabilidades.

1. **`UserService`**: Responsável por toda a lógica relacionada a utilizadores, contas e contactos.
    - **Métodos (Serviços que implementa):**
        - `register(UserInfo user, String password)`: Valida e regista um novo utilizador no banco de dados.
        - `login(String nickname, String password)`: Autentica um utilizador.
        - `searchUser(String nickname)`: Procura por um utilizador no sistema.
        - `addContact(ContactRequest request)`: Processa um pedido de adição de contacto.
        - `getContacts(String userNickname)`: Retorna a lista de contactos de um utilizador.
            
2. **`CallService`**: Responsável por gerir o ciclo de vida e o estado das chamadas e da presença dos utilizadores.
    - **Métodos (Serviços que implementa):**
        - `initiateCall(CallInvitation invitation)`: Inicia o processo de chamada, notificando o destinatário.
        - `acceptCall(String callId)`: Confirma que a chamada foi aceite e atualiza o estado dos utilizadores.
        - `refuseCall(String callId)`: Cancela uma chamada que foi recusada.
        - `endCall(String callId)`: Finaliza uma chamada em andamento e atualiza o estado dos utilizadores.
        - `updateUserStatus(String nickname, String newStatus)`: Altera o estado de presença de um utilizador.

---
### **2. Definindo Superclasse, Subclasses, Agregação e Interface**

#### Agregação
- **Ideia:** A classe **`User`** (que representa um utilizador no sistema) **tem uma** lista de contactos.    
- **Implementação Conceitual:**
    - Classe `User`
        - Atributo: `String nickname`.
        - Atributo: `String encryptedPassword`
        - Atributo: `List<User> contacts` <-- **AGREGAÇÃO AQUI**. Um utilizador é composto por seus dados e sua lista de contactos, que são outros objetos `User`.

#### **Interface**
- **Ideia:** Criar uma interface **`INotification`** que define o que toda notificação no sistema deve ser capaz de fazer.
- **Implementação Conceitual:**
    - Interface `INotification`
        - Método: `getNotificationType()` (retorna uma string como "CHAMADA_RECEBIDA" ou "PEDIDO_CONTACTO")
        - Método: `getMessage()` (retorna uma mensagem para o utilizador, ex: "Kauan está a ligar...")
    
- **Classes que implementam a interface:**    
	- `IncomingCallNotification` **implementa** `INotification`: Representa o alerta de uma chamada a chegar.
    - `ContactRequestNotification` **implementa** `INotification`: Representa o alerta de um novo pedido de amizade.        
    - `StatusChangeNotification` **implementa** `INotification`: Notifica que o estado de um contacto mudou.

#### **Superclasse e Subclasses (Herança - Relação "é-um-tipo-de")**

Aqui está a solução para a vossa dificuldade. Precisamos de uma abstração. Pense no coração do seu sistema: a comunicação. Uma chamada de voz é um tipo de "sessão de comunicação". No futuro, vocês poderiam querer adicionar chat por texto ou videochamadas.

- **Ideia:** Criar uma classe abstrata **`CommunicationSession`** que define características comuns a qualquer tipo de comunicação entre utilizadores. A chamada de voz será uma subclasse especializada.
    
- **Implementação Conceitual:**
    
    - **Superclasse (Abstrata): `CommunicationSession`**
        
        - **Atributos comuns:**
            
            - `String sessionId` (ID único da sessão)
                
            - `List<User> participants` (Lista de participantes)
                
            - `Date startTime` (Quando começou)
                
            - `Date endTime` (Quando terminou)
                
        - **Métodos comuns:**
            
            - `start()`
                
            - `end()`
                
    - **Subclasse (Concreta): `VoiceCallSession` herda de `CommunicationSession`**
        
        - Esta classe **é-um-tipo-de** `CommunicationSession`.
            
        - **Atributos específicos:**
            
            - `String audioCodec` (ex: Opus, G.711)
                
            - `int jitterBuffer`
                
        - **Métodos específicos (ou sobrescritos):**
            
            - `muteParticipant(User user)`
                
            - `unmuteParticipant(User user)`
                

Com esta estrutura, se um dia quisessem adicionar chat de texto, poderiam criar outra subclasse `TextMessageSession` que também herdaria de `CommunicationSession`, provando a utilidade e a lógica da herança.

Espero que estas ideias ajudem a estruturar o trabalho de acordo com os requisitos!