
A arquitetura utiliza um Servidor de Mídia (Media Relay) na camada de lógica, assegurando que a comunicação funcione de forma fiável em qualquer cenário de rede. O design distingue claramente o Plano de Controle (gerido via TCP) e o Plano de Dados (gerido via UDP), ambos orquestrados pela camada de lógica.

## 1. Detalhamento das Camadas e Tecnologias

#### Camada 1: Apresentação (Cliente)

**Componente**: Cliente VoIP Desktop.

**Linguagem Proposta:** C++. Essencial para aplicações em tempo real. C++ oferece o controlo de baixo nível necessário para a captura/reprodução de áudio com mínima latência, performance previsível (sem pausas de garbage collector) e acesso direto a bibliotecas de processamento de áudio (como o codec Opus).

**Responsabilidades:**
- Apresentar a Interface do Utilizador (GUI).
- Gerir a interação do utilizador (login, ligar, desligar).
- Comunicar com a Camada de Lógica (Sinalização) via TCP.
- Enviar e receber o fluxo de áudio (UDP) para/de a Camada de Lógica (Media Relay).

#### Camada 2: Lógica/Aplicação (Backend)
Esta camada é composta por dois serviços distintos, cada um com uma tecnologia otimizada para a sua função.

**Componente 2a**: Servidor de Sinalização

**Linguagem Proposta:** Python.Perfeito para tarefas de rede I/O-bound (entrada/saída). O desenvolvimento é extremamente rápido para a lógica de controlo, gestão de estado e manipulação de mensagens de texto/JSON do protocolo.

**Responsabilidades:**

- Gerir conexões TCP persistentes com os clientes.
- Orquestrar todo o ciclo de vida da chamada (INVITE, ACCEPT, BYE).
- Autenticar utilizadores, consultando a Camada de Dados.
- Manter o estado de cada utilizador (Disponível, Em Chamada, etc.).

**Componente 2b: Servidor de Mídia (Media Relay)**

Linguagem Proposta: C++.cEsta é uma tarefa de alta performance. O servidor precisa de reencaminhar milhares de pacotes UDP por segundo com a menor latência possível. 

**Responsabilidades:**
- Receber pacotes UDP de um cliente.
- Identificar a sessão da chamada.
- Reencaminhar (fazer o "relay") o pacote para o outro cliente na sessão.

#### Camada 3: Dados (Persistência)

**Componente**: Banco de Dados Relacional.

Tecnologia Proposta: PostgreSQL (para um sistema robusto) ou SQLite (para simplicidade).

Responsabilidades: Armazenar de forma segura os dados dos utilizadores (nomes, senhas criptografadas). Manter listas de contactos e outras informações persistentes. Fornecer uma fonte de verdade para a autenticação realizada pela Camada de Lógica.


2. Casos de Uso Principais
UC-01: Autenticação de Utilizador

Ator: Utilizador.

Fluxo: O utilizador abre o cliente, insere as credenciais. O Cliente (Apresentação) envia-as para o Servidor de Sinalização (Lógica). O Servidor valida as credenciais contra o Banco de Dados (Dados) e retorna sucesso ou falha.

UC-02: Realizar uma Chamada

Ator: Chamador.

Pré-condição: Ambos os utilizadores estão autenticados e online.

Fluxo: O Chamador seleciona um contacto e clica em "Ligar". O Cliente (Apresentação) envia uma mensagem INVITE para o Servidor de Sinalização (Lógica), que orquestra o convite para o outro utilizador.

UC-03: Encerrar uma Chamada

Ator: Qualquer utilizador na chamada.

Fluxo: O utilizador clica em "Desligar". O Cliente (Apresentação) envia uma mensagem BYE para o Servidor de Sinalização (Lógica), que informa o outro participante e atualiza o estado de ambos.

3. Exemplo Prático: Fluxo de uma Chamada Completa
Cenário: ana quer ligar para bia. Ambos estão em Quixadá e online.

Sinalização (Plano de Controle - TCP):

ana -> Cliente C++: Clica no botão para ligar para bia.

Cliente C++ de ana -> Servidor Python: Envia a mensagem INVITE bia.

Servidor Python: Recebe o convite. Verifica no seu estado interno que bia está Disponível.

Servidor Python -> Cliente C++ de bia: Envia a mensagem INCOMING_CALL ana.

Cliente C++ de bia: Exibe uma notificação: "Chamada de ana". bia clica em "Aceitar".

Cliente C++ de bia -> Servidor Python: Envia a mensagem ACCEPT ana.

Orquestração (O "Maestro" em Ação):

Servidor Python: Recebe o ACCEPT. Agora ele executa a lógica principal:

Atualiza o estado de ana e bia para EM_CHAMADA.

Envia uma mensagem para o Cliente de ana: CONNECT_MEDIA 203.0.113.10:9000 (o endereço do Servidor de Mídia C++/Go).

Envia a mesma mensagem para o Cliente de bia: CONNECT_MEDIA 203.0.113.10:9000.

Mídia (Plano de Dados - UDP):

Cliente C++ de ana: Abre um socket UDP e começa a enviar pacotes de áudio para o endereço do Servidor de Mídia.

Cliente C++ de bia: Faz exatamente o mesmo.

Servidor de Mídia C++/Go: A sua lógica entra num loop simples:

Recebe um pacote UDP do IP da ana. Sabe que esta sessão pertence à bia. Reencaminha o pacote para o IP da bia.

Recebe um pacote UDP do IP da bia. Sabe que esta sessão pertence à ana. Reencaminha o pacote para o IP da ana.

A conversa está a fluir, mediada pelo Servidor de Mídia.

Encerramento (Plano de Controle - TCP):

A chamada termina. bia clica em "Desligar".

Cliente C++ de bia -> Servidor Python: Envia a mensagem BYE.

Servidor Python: Atualiza o estado de ambos para Disponível e envia uma notificação CALL_ENDED para ana.

Ambos os clientes C++ param de enviar pacotes UDP. A chamada está oficialmente encerrada.