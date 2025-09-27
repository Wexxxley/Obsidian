

---

Os **modelos fundamentais** adotam uma perspectiva mais abstrata para entender e analisar propriedades essenciais dos sistemas distribuídos. Seu objetivo é:
- Tornar explícitas todas as suposições relevantes sobre o sistema.
- Fazer generalizações sobre o que é possível ou impossível, dadas essas suposições.

---
## **1. O Modelo de Interação**

Este modelo lida com o desempenho e a dificuldade de estabelecer limites de tempo em um sistema distribuído. Ele se concentra em dois fatores:

1. **Desempenho da Comunicação**: A comunicação em uma rede tem as seguintes características de desempenho:
    - **Latência**: O atraso entre o início do envio de uma mensagem e o início de sua recepção no destino. Inclui o tempo de propagação do sinal, atrasos de acesso à rede e tempo de processamento nos sistemas operacionais.
    - **Taxa de tranferência**: O volume total de informações que pode ser transmitido por uma rede em um determinado momento.
    - **Jitter**: A variação no tempo necessário para entregar uma série de mensagens. É um fator crucial para dados de multimídia, como áudio e vídeo.
        
2. **Inexistência de Relógio Global**: Cada computador em um sistema distribuído tem seu próprio relógio interno, mas esses relógios se desviam uns dos outros com o tempo. É impossível sincronizá-los perfeitamente devido aos atrasos variáveis da rede. Isso significa que não existe uma noção global única de tempo, o que complica a coordenação de ações que dependem do tempo.
    
Com base nesses fatores, o modelo de interação se divide em duas variantes opostas:

1. **Sistemas Distribuídos Síncronos**: Um sistema é síncrono se existem limites **conhecidos e finitos** para:
    - O tempo de execução de cada passo de um processo.
    - O tempo de entrega de cada mensagem transmitida.
    - A taxa de desvio do relógio de cada processo em relação ao tempo real.
        
2. **Sistemas Distribuídos Assíncronos**: Um sistema é assíncrono se **não existem limites** para a velocidade de execução dos processos, para os atrasos na transmissão de mensagens ou para as taxas de desvio do relógio. A Internet é um exemplo perfeito de um sistema assíncrono, pois uma mensagem de e-mail pode levar segundos ou dias para chegar. 

#### **Ordenação de Eventos**
Mesmo sem relógios perfeitamente sincronizados, é crucial saber se um evento ocorreu antes de outro. Para resolver isso, **relógios lógicos** (propostos por Lamport) podem ser usados para fornecer uma ordenação de eventos que não depende de relógios físicos, mas sim da relação causal de que uma mensagem deve ser recebida após ter sido enviada.

---
## **2. O Modelo de Falhas**

Este modelo define e classifica os diferentes tipos de falhas que podem ocorrer em um sistema distribuído. Ter uma classificação clara das falhas ajuda a analisar seus efeitos e a projetar sistemas que possam tolerá-las e continuar funcionando corretamente. 

1. **Falhas por Omissão**: Ocorrem quando um processo ou canal de comunicação deixa de executar uma ação que deveria.
    - **Falha de Processo**: Um processo para e permanece parado. Outros processos podem ou não conseguir detectar esse estado. Se for possível detectar com certeza que o processo parou, a falha é chamada de **parada por falha (fail-stop)**.
    - **Falha de Comunicação**: Ocorre quando uma mensagem é perdida durante a transmissão entre o buffer de envio do remetente e o buffer de recepção do destinatário.
        
2. **Falhas Arbitrárias**: Também conhecidas como **falhas Bizantinas**, representam o cenário onde qualquer tipo de erro pode ocorrer.
    - Um processo com falha arbitrária pode omitir passos, executar passos indesejados, atribuir valores incorretos aos seus dados ou retornar um valor errado.
    - Um canal de comunicação com falha arbitrária pode corromper mensagens, entregar mensagens inexistentes ou entregar a mesma mensagem mais de uma vez.
        
3. **Falhas de Temporização**: Estas falhas são aplicáveis apenas a **sistemas síncronos**, onde existem limites de tempo definidos.
    - **Falha de Relógio**: O relógio local de um processo excede os limites de sua taxa de desvio em relação ao tempo real.
    - **Falha de Desempenho**: Um processo ou canal de comunicação excede os limites de tempo definidos para executar uma tarefa ou entregar uma mensagem.

#### **Tolerância e Mascaramento de Falhas**

- **Mascaramento de Falhas**: Um serviço pode mascarar uma falha ocultando-a completamente ou convertendo-a em um tipo de falha mais aceitável. Por exemplo:
    - A retransmissão de mensagens pode mascarar a falha por omissão de um pacote perdido.
    - O uso de somas de verificação (checksums) pode converter uma falha arbitrária (mensagem corrompida) em uma falha por omissão (a mensagem corrompida é simplesmente descartada).
        
- **Comunicação Confiável**: ==Um serviço de comunicação é considerado confiável== se possui duas propriedades:
    - **Validade**: Qualquer ==mensagem enviada é entregue ao buffer== de recepção do destino.
    - **Integridade**: A mensagem recebida é ==idêntica à enviada==, e nenhuma mensagem é entregue duas vezes.

---
## **3. O Modelo de Segurança**

O modelo de segurança discute as possíveis ameaças aos processos e canais de comunicação e apresenta o conceito de um canal seguro para se proteger contra essas ameaças. A segurança de um sistema distribuído é obtida ao:
- Tornar seguros os processos e os canais usados para suas interações.
- Proteger os objetos que eles encapsulam contra o acesso não autorizado.

#### **3.1 Proteção de Objetos**
- **Direitos de Acesso**: Para proteger um recurso (como um objeto), o sistema especifica quem tem permissão para realizar determinadas operações sobre ele.
- **Principal**: Para gerenciar os direitos de acesso, o modelo introduz o conceito de **principal**, que é a identidade em nome da qual um processo está executando (geralmente um usuário ou outro processo). Um servidor é responsável por verificar a identidade do principal por trás de cada invocação e checar se ele tem direitos de acesso suficientes para a operação solicitada.

#### **3.2 Ameaças de um Invasor**
Para analisar as ameaças, o modelo postula a existência de um **invasor** que é capaz de enviar qualquer mensagem para qualquer processo e ler ou copiar qualquer mensagem que trafega na rede. As principais ameaças são:

- **Ameaças aos Processos**: Como a origem de uma mensagem pode ser falsificada, tanto servidores quanto clientes estão em risco.
    - Um **servidor** não pode ter certeza da identidade do principal por trás de uma requisição e pode, erroneamente, conceder acesso a um usuário não autorizado.
    - Um **cliente** não pode ter certeza de que uma mensagem de resposta veio do servidor correto; ela pode ter sido enviada por um invasor se passando pelo servidor.
        
- **Ameaças aos Canais de Comunicação**: Um invasor pode copiar, alterar ou injetar mensagens enquanto elas trafegam pela rede. Isso ameaça a **privacidade** e a **integridade**. Outro ataque é o de **replay**, onde um invasor salva mensagens e as reenvia mais tarde (por exemplo, reenviar uma requisição de transferência bancária).
    
- **Negação de Serviço**: Um ataque onde um usuário mal-intencionado impede que usuários legítimos utilizem um serviço, por exemplo, bombardeando o serviço com um número excessivo de requisições sem sentido.
    
#### **3.3 Anulando Ameaças com Canais Seguros**
As ameaças podem ser anuladas com o uso de **canais de comunicação seguros**. Um canal seguro é construído usando-se técnicas de criptografia e autenticação e possui as seguintes propriedades:

1. **Autenticação**: Cada um dos processos no canal conhece com certeza a identidade do principal em nome do qual o outro processo está executando.
2. **Privacidade e Integridade**: O canal garante a **privacidade** (por meio de criptografia) e a **integridade** que é garantida por meio de técnicas como assinaturas digitais, que permitem ao destinatário verificar que a mensagem não foi alterada desde que foi enviada.
3. **Proteção contra Replay**: Cada mensagem inclui uma indicação de tempo (lógico ou físico) para impedir que mensagens sejam reproduzidas ou reordenadas.