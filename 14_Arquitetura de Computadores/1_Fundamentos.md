

--- 
O hardware de um computador executa um ==conjunto limitado e simples de instruçoes: Soma, comparação, tranferência de dados de um parte da memória para outra, etc.==
### **1. Arquitetura de Von Neumann (1945)**

A Arquitetura de Von Neumann é o conceito teórico sobre o qual a maioria dos computadores é construída. 

1. **Unidade Central de Processamento (CPU):** 
    - **Unidade de Controle (UC):** Gerencia dados e interpreta instruções.
    - **Unidade Lógica e Aritmética (ULA):** Onde acontece os cálculos
    - **Registradores:** Pequenas memórias na CPU para armazenamento temporário.
2. **Memória Principal (RAM):** Espaço único que armazena instruções e dados.
3. **Sistemas de Entrada e Saída:** Dispositivos que permitem a interação com o externo.
4. **Barramento:** Um barramento externo compartilahdo interligando os componentes.

![](../attachments/Pasted%20image%2020260207131705.png)
**Ciclo de Instrução**:
- **Busca (Fetch):** A CPU busca a próxima instrução na memória principal.
- **Decodificação (Decode):** A UC interpreta o que aquela instrução pede.
- **Execução (Execute):** A ULA realiza a operação ou os dados são movimentados entre os componentes.

>[!note]
**Gargalo de Von Neumann**: Como existe apenas um barramento, a CPU precisa esperar que a memória entregue as informações. Hoje em dia, a velocidade de processamento da CPU cresceu muito mais rápido do que a velocidade de transferência de dados da memória, tornando a comunicação entre elas um limitador de desempenho.

---
### **2. Arquitetura de Harvard**

A Arquitetura de Harvard utiliza memórias e barramentos separados para dados e instruções. Isso permite que o processador leia uma instrução e acesse um dado simultaneamente, evitando o gargalo mencionado acima.

Isso reduz significamente o gargalo de Von Neumann, mas encarece o sistema como um todo.

![](../attachments/Pasted%20image%2020260207101716.png)


---
### **3. Máquina multinível**

O conceito de **Máquina Multinível** é uma abstração. Em vez de tentarmos ent  ender o computador como um emaranhado de elétrons e portas lógicas, nós o dividimos em **camadas de abstração**. Cada nível utiliza os serviços do nível inferior e oferece funcionalidades para o nível superior.

![500](../attachments/Pasted%20image%2020260207105956.png)
**Nível 5 -** Linguagens de alto nível.
**Nível 4 -** Linguagem de montagem. Tradução mnemônica do código de máquina.
**Nível 3 -** Gerencia recursos.
**Nível 2 -** O código de máquina real que o processa
**Nível 1 -** Onde os componentes da arquitetura de Von Neumann residem
**Nível 0 -** Portas lógicas e circuitos eletrônicos
