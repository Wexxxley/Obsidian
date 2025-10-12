
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

# 2. Requisitos

**UC-01: Autenticação de Utilizador** 
- **Objetivo:** Permitir que o utilizador aceda ao sistema de forma segura.
- **Fluxo:** O utilizador insere credenciais no Cliente → Cliente envia para Servidor de Sinalização (TCP) → Servidor consulta Banco de Dados → Servidor retorna sucesso/falha e atualiza o estado do utilizador para **`Online`**.

**UC-02: Iniciar uma Chamada**
- **Objetivo:** Estabelecer a sessão de sinalização e coordenar o início da transmissão de mídia.
- **Pré-condição:** Ambos os utilizadores estão autenticados e `Online`.
- **Fluxo Detalhado:**
    1. O Chamador clica em "Ligar".
    2. O Cliente do Chamador envia INVITE (via TCP) contendo seu endereço de conexão para o Servidor de Sinalização.
    3. O Servidor de Sinalização: Verifica o estado do Chamado →  Gera uma nova Sessão de Mídia (ID Único) para a chamada → Informa o Servidor de Mídia sobre esta nova sessão.
    4. O Servidor de Sinalização envia o INVITE para o Cliente do chamado.
    5. O Cliente do Chamado envia ACCEPT (via TCP) para o Servidor de Sinalização.
    6. O Servidor de Sinalização atualiza o estado de ambos para **`Em Chamada`** e reencaminha o `ACCEPT` para o Chamador.
    7. Ambos os Clientes começam a enviar áudio UDP para o Servidor de Mídia 

**UC-03: Encerrar uma Chamada**
- **Objetivo:** Finalizar a comunicação e liberar recursos.
- **Fluxo:** O Utilizador (A ou B) clica em "Desligar" → Cliente envia `BYE` para Servidor de Sinalização (TCP) → Servidor envia `BYE` para o outro Cliente e atualiza o estado de ambos para Online → Servidor informa o Servidor de Mídia para *destruir a Sessão de Mídia.

 **UC-04: Transmissão de Áudio**
- **Objetivo:** Transportar o fluxo de áudio em tempo real com baixa latência entre os dois clientes, utilizando o Media Relay.
- **Pré-condição:** A chamada foi estabelecida com sucesso (UC-02 concluído) e o Servidor de Mídia tem uma sessão ativa.
- **Fluxo Detalhado:**
    1. O Cliente (A) capta e empacota o áudio num pacote UDP.
    2. O Cliente (A) envia o pacote UDP para o Servidor de Mídia, incluindo o ID da Sessão.
    3. O Servidor de Mídia recebe o pacote UDP e utiliza o ID da Sessão e a porta de origem do pacote para identificar o Cliente de destino (Cliente B).
    4. O Servidor de Mídia reencaminha o pacote UDP para o endereço do Cliente B.
    5. O Cliente B recebe o pacote, desempacota e reproduz o áudio.
    6. Este fluxo ocorre em simultâneo e continuamente em ambas as direções (A ↔ B) até o UC-03.

 **UC-05: Registo de Novo Utilizador**
- **Objetivo:** Criar um novo registo de utilizador.
- **Fluxo:** Utilizador insere dados de registo no Cliente → Cliente envia `REGISTO` para Servidor de Sinalização (TCP) → Servidor valida e persiste no Banco de Dados.

**UC-06: Gestão de Presença e Contactos**
- **Objetivo:** Fornecer visibilidade sobre o estado dos contactos.
- **Fluxo Principal:** Cliente solicita lista e estados ao Servidor de Sinalização após login → Servidor retorna lista/estados → Quando o estado muda, Servido envia proativamente `STATUS_UPDATE` para Clientes subscritos (os que têm o utilizador na lista).


Com certeza! A sua análise está correta. O material que você preparou é excelente e contém todos os detalhes técnicos necessários, mas mistura os **"o quês"** (requisitos) com os **"comos"** (detalhes do fluxo e da implementação).

Vamos separar e organizar isso de forma mais estruturada, seguindo as boas práticas de engenharia de software. Dividiremos o documento em três partes claras:

1. **Requisitos Funcionais (RF):** O que o sistema **deve fazer**. São declarações de capacidade.
    
2. **Requisitos Não-Funcionais (RNF):** Como o sistema **deve ser**. São os critérios de qualidade (desempenho, segurança, etc.).
    
3. **Casos de Uso (UC):** Como um ator (utilizador) **interage** com o sistema para atingir um objetivo.
    

---


#### **1. Requisitos Funcionais (RF)**

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
- **`RF-04.4 (Novo):`** O sistema deve permitir que um utilizador procure outros utilizadores registados no sistema (ex: por nome de utilizador).
    
- **`RF-04.5 (Novo):`** O sistema deve permitir que um utilizador envie um pedido de adição de contacto a outro utilizador.
    
- **`RF-04.6 (Novo):`** O sistema deve permitir que um utilizador aceite ou recuse um pedido de adição de contacto recebido.
    
- **`RF-04.7 (Novo):`** O sistema deve adicionar os utilizadores às listas de contacto um do outro apenas após a aceitação do pedido.
    - 
        
- **RF-05: Comunicação por Voz**
    
    - `RF-05.1:` O sistema deve permitir que um utilizador inicie uma chamada de voz com outro utilizador que esteja com o estado `Online`.
        
    - `RF-05.2:` O sistema deve permitir que um utilizador receba e aceite ou recuse um convite para uma chamada de voz.
        
    - `RF-05.3:` O sistema deve permitir que qualquer um dos participantes encerre uma chamada de voz a qualquer momento.
        
    - `RF-05.4:` O sistema deve transmitir o áudio entre os participantes durante uma chamada ativa.
        

#### **2. Requisitos Não-Funcionais (RNF)**

Estes são os critérios que definem a qualidade da operação do sistema.

- **RNF-01: Desempenho**
    
    - A latência na transmissão de áudio (ponta a ponta) deve ser suficientemente baixa para permitir uma conversação natural (geralmente abaixo de 200ms).
        
- **RNF-02: Segurança**
    
    - As credenciais do utilizador devem ser armazenadas e transmitidas de forma segura.
        
    - A comunicação de sinalização deve ocorrer sobre um canal seguro (ex: TCP com TLS).
        
- **RNF-03: Disponibilidade**
    
    - Os serviços de sinalização e de mídia devem estar disponíveis para uso contínuo, com o mínimo de tempo de inatividade.
        
- **RNF-04: Escalabilidade**
    
    - A arquitetura deve ser capaz de suportar um número crescente de utilizadores e chamadas simultâneas.
        

---

#### **3. Casos de Uso (UC)**

Aqui descrevemos a interação passo a passo entre o utilizador e o sistema.

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
        
    4. O sistema valida as credenciais, estabelece a sessão do utilizador, define seu estado para `Online` e apresenta a interface principal (ex: lista de contactos).
        
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
    
    - **Utilizador Chamado Recusa a Chamada:** No passo 4, se o Utilizador Chamado selecionar "Recusar", o sistema informa o Chamador da recusa e a chamada não é estabelecida. O estado de ambos permanece `Online`.
        
    - **Utilizador Chamado Não Atende:** No passo 3, se o Utilizador Chamado não responder dentro de um tempo limite, o sistema cancela o convite, informa o Chamador e a chamada não é estabelecida.
        
    - **Utilizador Chamado está Ocupado:** No passo 1, se o Utilizador Chamador tentar ligar para alguém que já está `Em Chamada`, o sistema o informa imediatamente que o contacto está ocupado.