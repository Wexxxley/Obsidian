

---
A ideia é permitir que um programa cliente chame um procedimento em um servidor remoto **como se fosse um procedimento local**. O sistema de RPC, atuando como middleware, oculta todos os detalhes complexos da distribuição, como:
- Empacotamento dos parâmetros da chamada em uma mensagem.
- A transmissão dessa mensagem de requisição ao servidor.
- O recebimento da mensagem de resposta.
- Desempacotamento dos resultados.

#### **Questões de Projeto para RPC**

**1. Programação com Interfaces**
- Em sistemas distribuídos, os módulos (cliente e servidor) executam-se em processos distintos. Um servidor fornece uma **interface de serviço**.
    
- Para permitir que programas escritos em linguagens diferentes se comuniquem, os sistemas RPC usam uma **IDL - Interface Definition Language**.
    
- Uma IDL é uma notação neutra usada para definir os procedimentos, seus parâmetros (especificando se são de **entrada (in)**, **saída (out)** ou **ambos (inout)**) e seus tipos de retorno.
    
- Como os processos estão em espaços de endereçamento diferentes, a passagem de parâmetros por "referência" não é suportada. Os parâmetros são passados por valor.   

**2. Semântica de Chamada RPC** Como a RPC é construída sobre protocolos de requisição-resposta que podem falhar, ela não pode garantir a mesma semântica "exatamente uma vez" de uma chamada local. O livro define três semânticas possíveis:

- **Semântica _talvez_**: A chamada remota pode ser executada uma vez ou não ser executada. Ocorre se nenhuma medida de tolerância a falhas for aplicada (por exemplo, se o cliente não retransmitir uma requisição perdida).
    
- **Semântica _pelo menos uma vez_**: O cliente recebe um resultado (sabendo que o procedimento foi executado pelo menos uma vez) ou uma exceção (informando que nenhum resultado foi recebido). Isso é obtido pela retransmissão de mensagens de requisição. O risco é que operações não idempotentes (como "sacar R$ 100") podem ser executadas várias vezes se a resposta for perdida e o cliente retransmitir.
    
- **Semântica _no máximo uma vez_**: O cliente recebe um resultado (sabendo que o procedimento foi executado exatamente uma vez) ou uma exceção (sabendo que o procedimento foi executado zero ou uma vez). Esta é a semântica mais forte e desejável. Ela é obtida usando todas as medidas de tolerância a falhas: retransmissão de requisições, filtragem de duplicatas no servidor e retransmissão de respostas (usando um histórico).
    

**3. Transparência**

- O objetivo original da RPC era fornecer **transparência de acesso e localização**, fazendo com que a chamada remota fosse sintaticamente idêntica a uma chamada local.
    
- No entanto, o livro aponta que essa transparência **não é total** e pode ser enganosa. Chamadas remotas são fundamentalmente diferentes das locais porque:
    
    - Estão sujeitas a **falhas de rede e de processos remotos** (falhas parciais).
        
    - Têm uma **latência significativamente maior**.
        
    - Não suportam passagem de parâmetros por referência (ponteiros de memória).
        
- Portanto, o consenso atual é que, embora a _sintaxe_ da chamada deva ser transparente, a _interface_ do serviço remoto deve deixar claro que se trata de uma operação distribuída, por exemplo, disparando exceções específicas de rede.
    

#### **Implementação de RPC (Seção 5.3.2)**

A RPC é implementada usando componentes de software gerados automaticamente a partir da definição da IDL:

- **Stub do Cliente (Client Stub)**: Um procedimento que é executado no cliente. Ele se parece com o procedimento remoto real, mas sua única função é empacotar (marshal) os argumentos em uma mensagem de requisição e enviá-la ao servidor. Em seguida, ele espera pela resposta, desempacota os resultados e os retorna ao programa cliente.
    
- **Módulo de Comunicação**: Lida com a transmissão de mensagens (requisições e respostas) entre o cliente e o servidor, implementando a semântica de chamada desejada (ex: retransmissões).
    
- **Despachante (Dispatcher)**: Executado no servidor. Ele recebe a mensagem de requisição, examina o identificador do procedimento e chama o esqueleto do servidor correspondente.
    
- **Esqueleto do Servidor (Server Skeleton)**: Um procedimento no servidor. Sua função é desempacotar os argumentos da mensagem de requisição, chamar o procedimento de serviço real (a implementação) e, em seguida, empacotar os resultados em uma mensagem de resposta para enviar de volta ao cliente.
    

O **Sun RPC** é apresentado como um estudo de caso que utiliza a linguagem XDR como IDL e pode ser executado sobre UDP (com semântica "pelo menos uma vez") ou TCP