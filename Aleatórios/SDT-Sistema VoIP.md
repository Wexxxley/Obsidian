


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

# **5. Definições de POO**
#### **Classes POJO (Plain Old Java Objects)**

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
### **Definindo Superclasse, Subclasses, Agregação e Interface**

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

#### **Superclasse e Subclasses**
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
        - **Atributos específicos:**
            - `String audioCodec` (ex: Opus, G.711)
            - `int jitterBuffer`
                
        - **Métodos específicos (ou sobrescritos):**
            - `muteParticipant(User user)`    
            - `unmuteParticipant(User user)`


Com esta estrutura, se um dia quisessem adicionar chat de texto, poderiam criar outra subclasse `TextMessageSession` que também herdaria de `CommunicationSession`, provando a utilidade e a lógica da herança.



Claro! Com base no detalhado documento de arquitetura (`SDT-Sistema VoIP.md`) que você forneceu, podemos estruturar a criação da interface do cliente.

A combinação de Electron com C++ é uma abordagem poderosa:

- **Electron** será usado para construir a interface de utilizador (GUI) de forma rápida e moderna, utilizando tecnologias web (HTML, CSS, JavaScript).
    
- **C++** será o "motor" de baixo nível, responsável pelas tarefas críticas de performance como a comunicação de rede (TCP para sinalização, UDP para áudio) e o processamento de áudio. A comunicação entre o JavaScript do Electron e o C++ é feita através de um **Node.js Addon**.
    

Vamos estruturar o projeto e criar o código para as interfaces que você desenhou.

### 1. Estrutura de Pastas do Projeto

Uma boa organização ajuda a separar as responsabilidades. Recomendo a seguinte estrutura:

```
/seu-projeto-voip
|
|-- /src
|   |-- main.js             # Ponto de entrada, processo principal do Electron
|   |-- preload.js          # Script para expor APIs do Node.js de forma segura para a GUI
|   |
|   |-- /assets             # CSS, imagens, etc.
|   |   |-- style.css
|   |
|   |-- /views              # Arquivos HTML para as janelas
|       |-- auth.html       # Janela de Autenticação (login e registo)
|       |-- main.html       # Janela Principal (lista de contactos, etc.)
|
|-- /cpp_addon              # Código do seu backend em C++
|   |-- binding.gyp         # Arquivo de build para o addon
|   |-- voip_backend.cc     # Lógica C++ de rede e áudio
|   |-- ...
|
|-- package.json            # Dependências e scripts do projeto
```

---

### 2. Configuração do Ambiente Electron

**1. Inicie o projeto e instale o Electron:**

Bash

```
# Crie a pasta e inicie o projeto npm
mkdir seu-projeto-voip
cd seu-projeto-voip
npm init -y

# Instale o Electron como dependência de desenvolvimento
npm install --save-dev electron
```

2. Configure o package.json:

Abra o package.json e modifique-o para que se pareça com isto, adicionando o main e o script start:

JSON

```
{
  "name": "seu-projeto-voip",
  "version": "1.0.0",
  "description": "Cliente VoIP para o trabalho de SD",
  "main": "src/main.js",
  "scripts": {
    "start": "electron ."
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "electron": "^21.0.0" // A versão pode variar
  }
}
```

3. Crie o Processo Principal (src/main.js):

Este ficheiro é o coração da sua aplicação desktop. Ele cria as janelas e lida com eventos do sistema.

JavaScript

```
// src/main.js
const { app, BrowserWindow, ipcMain } = require('electron');
const path = require('path');

let authWindow;
let mainWindow;

function createAuthWindow() {
  authWindow = new BrowserWindow({
    width: 400,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  });

  authWindow.loadFile('src/views/auth.html');
}

function createMainWindow() {
  mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  });

  mainWindow.loadFile('src/views/main.html');
}

app.whenReady().then(() => {
  createAuthWindow();

  app.on('activate', () => {
    if (BrowserWindow.getAllWindows().length === 0) {
      createAuthWindow();
    }
  });
});

// Ouve o evento de login bem-sucedido da janela de autenticação
ipcMain.on('login-success', () => {
  if (authWindow) {
    authWindow.close();
  }
  createMainWindow();
});

app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') {
    app.quit();
  }
});
```

---

### 3. Código da Interface Gráfica (GUI)

Agora, vamos criar os arquivos HTML, CSS e JavaScript para a GUI, seguindo exatamente o que foi definido na secção "GUI" do seu documento.

#### **Janela de Autenticação**

**`src/views/auth.html`**

HTML

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Acervo Mestre - Autenticação</title>
    <link rel="stylesheet" href="../assets/style.css">
</head>
<body>
    <div class="container">
        <div id="login-form">
            <h1>Login</h1>
            <input type="text" id="login-nickname" placeholder="Nickname">
            <input type="password" id="login-password" placeholder="Senha">
            <button id="login-btn">Entrar</button>
            <p id="login-error-msg" class="error-msg"></p>
            <a href="#" id="show-register-link">Ainda não tem conta? Registe-se</a>
        </div>

        <div id="register-form" style="display: none;">
            <h1>Criar Conta</h1>
            <input type="text" id="register-nickname" placeholder="Nickname desejado">
            <input type="password" id="register-password" placeholder="Senha">
            <input type="password" id="register-confirm-password" placeholder="Confirme a Senha">
            <button id="register-btn">Criar Conta</button>
            <p id="register-msg" class="error-msg"></p>
            <a href="#" id="show-login-link">Já tem uma conta? Faça o login</a>
        </div>
    </div>

    <script>
        // Lógica simples para alternar entre os formulários
        const loginForm = document.getElementById('login-form');
        const registerForm = document.getElementById('register-form');
        const showRegisterLink = document.getElementById('show-register-link');
        const showLoginLink = document.getElementById('show-login-link');

        showRegisterLink.addEventListener('click', (e) => {
            e.preventDefault();
            loginForm.style.display = 'none';
            registerForm.style.display = 'block';
        });

        showLoginLink.addEventListener('click', (e) => {
            e.preventDefault();
            registerForm.style.display = 'none';
            loginForm.style.display = 'block';
        });

        // Lógica de Autenticação (Exemplo)
        document.getElementById('login-btn').addEventListener('click', () => {
            const nickname = document.getElementById('login-nickname').value;
            const password = document.getElementById('login-password').value;

            // TODO: Chamar a função C++ para autenticar via 'window.api'
            // Ex: const result = await window.api.login(nickname, password);
            console.log(`Tentando login com: ${nickname}`);
            
            // Simulação de sucesso para demonstração
            if (nickname && password) {
                 // Envia uma mensagem para o processo principal para trocar de janela
                window.electron.send('login-success');
            } else {
                document.getElementById('login-error-msg').innerText = "Nickname ou senha inválidos.";
            }
        });
    </script>
</body>
</html>
```

#### **Janela Principal**

**`src/views/main.html`**

HTML

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Acervo Mestre - Principal</title>
    <link rel="stylesheet" href="../assets/style.css">
</head>
<body>
    <div class="main-container">
        <header>
            <div id="user-info">
                <span class="status-indicator online"></span>
                <span id="user-nickname">MeuNickname</span>
            </div>
            <button id="logout-btn">Logout</button>
        </header>

        <main>
            <div class="contacts-panel">
                <div class="panel-header">
                    <h2>Contatos</h2>
                    <button id="add-contact-btn">+</button>
                </div>
                <ul id="contact-list" class="contact-list">
                    </ul>
            </div>
        </main>
    </div>

    <div id="incoming-call-dialog" class="dialog-overlay" style="display: none;">
        <div class="dialog-box">
            <h3 id="caller-id-label"></h3>
            <div class="dialog-buttons">
                <button id="accept-call-btn">Aceitar</button>
                <button id="refuse-call-btn">Recusar</button>
            </div>
        </div>
    </div>
    
    <script>
        // Dados de exemplo (viriam do seu backend C++)
        const contacts = [
            { nickname: 'Kauan', status: 'Online' },
            { nickname: 'Ana', status: 'Em Chamada' },
            { nickname: 'Carlos', status: 'Offline' }
        ];

        const contactList = document.getElementById('contact-list');

        function renderContacts() {
            contactList.innerHTML = ''; // Limpa a lista
            for (const contact of contacts) {
                const statusClass = contact.status.toLowerCase().replace(' ', '-');
                
                const contactItem = document.createElement('li');
                contactItem.innerHTML = `
                    <div class="contact-info">
                        <span class="status-indicator ${statusClass}"></span>
                        <span class="contact-nickname">${contact.nickname}</span>
                    </div>
                    <button class="call-btn" ${contact.status !== 'Online' ? 'disabled' : ''}>Ligar</button>
                `;
                contactList.appendChild(contactItem);
            }
        }
        
        // Simulação de chamada recebida
        function showIncomingCall(callerNickname) {
            document.getElementById('caller-id-label').innerText = `${callerNickname} está a ligar...`;
            document.getElementById('incoming-call-dialog').style.display = 'flex';
        }

        // Renderiza a lista inicial
        renderContacts();
        
        // Exemplo de como mostrar o diálogo de chamada
        // setTimeout(() => showIncomingCall('Kauan'), 5000); // Teste após 5s
    </script>
</body>
</html>

```

#### **Folha de Estilos**

**`src/assets/style.css`**

CSS

```
/* Estilos Gerais */
body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; background: #f0f2f5; margin: 0; }
.container { padding: 20px; max-width: 360px; margin: 50px auto; background: white; border-radius: 8px; box-shadow: 0 2px 4px rgba(0,0,0,0.1); }
h1 { text-align: center; color: #333; }
input[type="text"], input[type="password"] { width: calc(100% - 20px); padding: 10px; margin-bottom: 15px; border: 1px solid #ddd; border-radius: 4px; }
button { width: 100%; padding: 10px; border: none; border-radius: 4px; background-color: #007bff; color: white; font-size: 16px; cursor: pointer; }
button:hover { background-color: #0056b3; }
button:disabled { background-color: #a0a0a0; cursor: not-allowed; }
a { color: #007bff; text-decoration: none; display: block; text-align: center; margin-top: 15px; }
.error-msg { color: #d93025; text-align: center; min-height: 20px; }

/* Janela Principal */
.main-container { display: flex; flex-direction: column; height: 100vh; }
header { display: flex; justify-content: space-between; align-items: center; padding: 10px 20px; background: #fff; border-bottom: 1px solid #ddd; }
#user-info { display: flex; align-items: center; gap: 8px; }
.contacts-panel { padding: 20px; }
.panel-header { display: flex; justify-content: space-between; align-items: center; }
#add-contact-btn { width: 30px; height: 30px; font-size: 20px; line-height: 30px; text-align: center; padding: 0; }

/* Lista de Contatos */
.contact-list { list-style: none; padding: 0; margin-top: 20px; }
.contact-list li { display: flex; justify-content: space-between; align-items: center; padding: 10px; border-bottom: 1px solid #eee; }
.contact-info { display: flex; align-items: center; gap: 10px; }
.call-btn { width: auto; padding: 5px 15px; font-size: 14px; }

/* Indicador de Status */
.status-indicator { width: 12px; height: 12px; border-radius: 50%; }
.status-indicator.online { background-color: #28a745; } /* Verde */
.status-indicator.offline { background-color: #6c757d; } /* Cinza */
.status-indicator.em-chamada { background-color: #dc3545; } /* Vermelho */

/* Diálogos */
.dialog-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.5); display: flex; justify-content: center; align-items: center; }
.dialog-box { background: white; padding: 25px; border-radius: 8px; text-align: center; }
.dialog-buttons { margin-top: 20px; display: flex; gap: 15px; }
```

#### **Script de Preload**

src/preload.js

Este arquivo é crucial para a segurança. Ele expõe funcionalidades do Node.js (como o ipcRenderer para comunicação entre janelas) de forma controlada.

JavaScript

```
// src/preload.js
const { contextBridge, ipcRenderer } = require('electron');

contextBridge.exposeInMainWorld('electron', {
  send: (channel, data) => {
    ipcRenderer.send(channel, data);
  }
  // Você também pode expor funções que recebem dados do processo principal
  // on: (channel, func) => {
  //   ipcRenderer.on(channel, (event, ...args) => func(...args));
  // }
});
```

---

### 4. Integração com o Backend C++

Esta é a parte mais complexa. O seu código JavaScript (nos arquivos `.html`) não pode chamar o C++ diretamente. Ele precisa de uma ponte.

1. **Criação do Addon C++:** Você usará `node-gyp` para compilar seu código C++ (`voip_backend.cc`) em um arquivo `.node` que o Node.js pode carregar com `require()`.
    
2. **Exposição de Funções:** Dentro do seu C++, você usará a API do Node.js (preferencialmente a N-API por ser mais estável) para expor suas funções (como `login`, `register`, `initiateCall`, etc.) para o JavaScript.
    
3. **Comunicação Assíncrona:** Operações de rede não podem bloquear a interface. O seu C++ precisará rodar a lógica de rede em threads separadas e usar `ThreadSafeFunction` (da N-API) para notificar a interface sobre eventos, como uma chamada recebida ou a mudança de status de um contato.
    

**Exemplo conceitual de como o JavaScript chamaria o C++:**

No seu `preload.js`, você carregaria o addon e o exporia de forma segura:

JavaScript

```
// src/preload.js (versão estendida)
const { contextBridge, ipcRenderer } = require('electron');
// Carrega o addon C++ compilado
const voipBackend = require('../cpp_addon/build/Release/voip_addon.node');

contextBridge.exposeInMainWorld('api', {
  // Exemplo de uma chamada síncrona
  login: (nickname, password) => voipBackend.login(nickname, password),

  // Exemplo de uma chamada assíncrona
  initiateCall: (calleeNickname) => voipBackend.initiateCall(calleeNickname),

  // Função para registar um callback que será chamado pelo C++
  onIncomingCall: (callback) => voipBackend.registerIncomingCallCallback(callback)
});

// ... (código anterior com 'electron.send')
```

E no seu HTML (`auth.html` ou `main.html`), você usaria assim:

JavaScript

```
// Exemplo de uso no script do auth.html
const result = window.api.login('meunick', '1234');
if (result.success) {
    window.electron.send('login-success');
} else {
    document.getElementById('login-error-msg').innerText = result.message;
}

// Exemplo de uso no script do main.html para receber chamadas
window.api.onIncomingCall((caller) => {
    // A função 'showIncomingCall' que criamos antes
    showIncomingCall(caller.nickname); 
});
```

### Próximos Passos

1. **Execute a Interface:** Rode `npm start` no seu terminal. A janela de login/registo deve aparecer.
    
2. **Desenvolva o Addon C++:** Este é o seu próximo grande passo. Foque em:
    
    - Configurar o `binding.gyp`.
        
    - Criar uma função simples (ex: uma que soma dois números) para testar a comunicação entre JS e C++.
        
    - Implementar a lógica de rede TCP/UDP para se comunicar com os seus servidores de Sinalização e Mídia.
        
3. **Conecte a GUI ao Addon:** Substitua a lógica de simulação nos arquivos HTML pela chamada real às funções do seu addon C++, como mostrado no exemplo conceitual acima.