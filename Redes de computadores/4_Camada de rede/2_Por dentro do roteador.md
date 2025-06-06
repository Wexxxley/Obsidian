
#Concluded 

---
### **1. Por dentro de roteador**
![[Pasted image 20250522195916.png]]
- **Portas de entrada**.
- **Elemento de comutação**. O elemento de comutação move os pacotes da entrada do roteador para a saída apropriada.
- **Portas de saída.** Uma porta de saída armazena os pacotes que foram repassados a ela e os transmite até o enlace de saída, realizando as funções necessárias da camada de enlace e da camada físico
- **Processador de roteamento.** O processador de roteamento executa os protocolos de roteamento, mantém as tabelas de roteamento e as informações de estado do enlace, e calcula a tabela de repasse para o roteador. 

---
#### **1.1 Funções da porta de entrada**
![[Pasted image 20250522200227.png]]
1. **Terminação de linha**: Responsável por **receber sinais físicos** vindos de uma interface de rede. Converte esses sinais em **bits**.
2. **Processamento de enlace:** Aqui ocorre o **desencapsulamento da camada de enlace**. Extrai o quadro recebido e verifica seu conteúdo. Remove o cabeçalho da camada de enlace.
3. **Consulta, repasse, fila**: Esta é a parte da camada de rede. O roteador consulta sua tabela de roteamento para decidir para onde o pacote deve ser enviado.
    - Pode **enfileirar** se a saída estiver ocupada.

---
#### **1.2 Elemento de comutação**
![[Pasted image 20250522201358.png]]

É por meio do elemento de comutação que os pacotes são comutados de uma porta de entrada para uma porta de saída. A comutação pode ser realizada de inúmeras maneiras:
##### 1. **Comutação via Memória**
- Os pacotes entram por uma interface e são **copiados para a memória central** do roteador.
- A CPU acessa os dados, processa o cabeçalho e determina a interface de saída.
- O pacote é copiado **para a interface de saída**.

- Simples de implementar.
- Limitado pela **velocidade do processador**. E pode causar gargalo em tráfego alto, pois apenas um pacote pode ser lido/escrito por vez.
##### 2. **Comutação via Barramento**
- Um **barramento compartilhado** conecta todas as interfaces.
- Quando um pacote chega à interface, ele é colocado no barramento e enviado para a interface de saída.
- **Apenas uma transmissão pode ocorrer por vez** no barramento. ==Problema de contenção==

- Mais rápido que o modelo com memória.
- Ainda há limitação: **uma única transferência por vez** no barramento.
##### 3. **Crossbar** 
- Usa uma **malha de conexões** que permite **várias transmissões simultâneas**, desde que não haja conflito de destino.

- Muito mais escalável e rápida.    
- Permite **transmissões paralelas**, ideal para **roteadores de alta performance**.
- Mais cara e complexa de implementar.

##### **Bloqueio head of the line** 
Problema que acontece quando o primeiro pacote de uma fila impede que outros pacotes atrás dele sejam transmitidos, mesmo que esses pacotes possam ser encaminhados.

Imagine uma fila de pacotes aguardando para sair por diferentes interfaces. Porém, os pacotes têm que sair na ordem de chegada.
1. O **pacote 1** está no início da fila e precisa sair pela **porta X**, que está **ocupada**.
2. O **pacote 2** está logo atrás e quer ir para a **porta Y**, que está **livre**.

Resultado: a **fila inteira fica bloqueada**, mesmo tendo pacotes que poderiam ser transmitidos.

---
#### **1.3 Processamento de saída**
![[Pasted image 20250522203955.png]]
##### 1.**Fila (gerenciamento de buffer)**
- Quando o pacote chega à saída, ele **pode ter que esperar** se a interface de transmissão estiver ocupada. Se o buffer estiver cheio, os pacotes **podem ser descartados**.
- [[15_Tipos de filas]]
##### 2. **Processamento de enlace
- Aqui, o pacote IP é **encapsulado novamente** em um **quadro de camada de enlace**.
##### 3. **Terminação de linha**
- A etapa final: **conversão dos dados digitais** para sinais físicos.
- [[5_Perdas e atrasos]]
