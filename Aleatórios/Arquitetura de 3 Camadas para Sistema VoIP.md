
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

# 2. CASOS DE USO

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


