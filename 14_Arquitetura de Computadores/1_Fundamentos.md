

--- 
O hardware de um computador executa um conjunto limitado e simples de instruçoes: Soma, comparação, tranferência de dados de um parte da memória para outra, etc.

### **1. Arquitetura de Von Neumann (1945)**

A Arquitetura de Von Neumann é o conceito teórico sobre o qual a maioria dos computadores é construída. 

1. **Unidade Central de Processamento (CPU):** 
    - **Unidade de Controle (UC):** Gerencia dados e interpreta instruções.
    - **Unidade Lógica e Aritmética (ULA):** Onde os cálculos matemáticos e operações lógicas acontecem.
    - **Registradores:** Pequenas memórias ultravelozes dentro da CPU para armazenamento temporário imediato.
2. **Memória Principal (RAM):** Espaço único que armazena instruções e dados.
3. **Sistemas de Entrada e Saída:** Dispositivos que permitem a interação com o mundo externo (teclado, monitor, discos).
4. **Barramento:** Um barramento externo compartilahdo interligando todos os componentes.
![500](../attachments/Pasted%20image%2020260207100406.png)

**Ciclo de Instrução**:
- **Busca (Fetch):** A CPU busca a próxima instrução na memória principal.
- **Decodificação (Decode):** A UC interpreta o que aquela instrução pede.
- **Execução (Execute):** A ULA realiza a operação ou os dados são movimentados entre os componentes.

>[!notw]
**Gargalo de Von Neumann**: Como existe apenas um barramento, a CPU precisa esperar que a memória entregue as informações. Hoje em dia, a velocidade de processamento da CPU cresceu muito mais rápido do que a velocidade de transferência de dados da memória, tornando a comunicação entre elas um limitador de desempenho.

## Von Neumann vs. Harvard

Diferente da arquitetura de Von Neumann, a **Arquitetura Harvard** utiliza memórias e barramentos separados para dados e instruções. Isso permite que o processador leia uma instrução e acesse um dado simultaneamente, evitando o gargalo mencionado acima. Ela é muito comum em sistemas embarcados e microcontroladores (como o Arduino).

---

Como você está estudando **Ciência da Computação** e já teve contato com Teoria da Computação e Sistemas Distribuídos, esse conceito é a base para entender por que otimizações de cache e pipeline são tão cruciais hoje em dia.

Gostaria que eu explicasse como os computadores modernos tentam "burlar" esse gargalo usando memórias cache ou execução fora de ordem?
 