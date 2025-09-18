

---
## O que é um Sistema Distribuído?

Um **Sistema Distribuído** é uma coleção de **computadores independentes** (hardware e software) interligados por uma rede que **se comunicam e coordenam suas ações apenas através da troca de mensagens**.

Em termos simples: é um grupo de máquinas trabalhando juntas como se fossem um único sistema, mesmo estando separadas fisicamente.

## Consequências Chave

### 1. Concorrência
Múltiplas tarefas e programas podem ser executados **simultaneamente** em diferentes computadores, compartilhando recursos (como arquivos ou serviços) quando necessário. Isso permite que o sistema **escale**, adicionando mais máquinas para aumentar a capacidade de processamento.
### 2. Inexistência de Relógio Global
Não existe um tempo único e perfeitamente sincronizado para todo o sistema. A coordenação entre os programas depende da troca de mensagens, e o tempo que essas mensagens levam na rede (latência) impede uma sincronização perfeita. Por isso, as ações são coordenadas por meio de **eventos** e **mensagens**, não por um relógio central.
### 3. Falhas Independentes
Componentes individuais (computadores, programas ou partes da rede) podem **falhar isoladamente** sem que todo o sistema pare. Quando uma máquina falha, as outras continuam operando. Os programas têm dificuldade em distinguir se um componente falhou ou se apenas a rede está lenta. Isso torna a **tolerância a falhas** um desafio e uma prioridade no projeto.
