
#Concluded 

---
Se um Processo é o "canteiro de obras", uma Thread é um trabalhador dentro desse canteiro. Um processo sempre começa com pelo menos uma thread. Mas ele pode criar várias outras para dividir o trabalho.

### **1. Por que usar Threads?** 

- **Processos são "pesados":**
    - Criar um processo novo é lento. O SO precisa alocar um novo espaço de memória, criar o PCB(Process Control Block), carregar o código, etc.
    - A troca de um Processo A para um Processo B é caro. O SO precisa salvar todo o contexto de A e carregar todo o contexto de B.
        
- **Threads são "leves":**
    - Criar uma nova thread é muito rápido. Por quê? Porque <mark style="background: #ADCCFFA6;">ela reaproveita a memória e os recursos do processo que a criou</mark>.
    - Trocar da Thread 1 para a Thread 2 é barato. O SO só precisa salvar os registradores e o ponteiro da stack da Thread 1 e carregar os da Thread 2. 
        

---
### **2. A Anatomia da Thread**

Todas as Threads do mesmo Processo **COMPARTILHAM**:

- **Espaço de Endereçamento:**
    - **Code Segment:** Todas leem o mesmo código do programa.
    - **Data Segment: T**odas acessam as mesmas variáveis globais.
    - **Heap:** Todas podem acessar e modificar os mesmos blocos de memória dinâmica.
        
- **Recursos do SO:**
    - **File Descriptors:** Se a Thread 1 abre um arquivo, a Thread 2 pode ler e escrever nele.
    - **Conexões de Rede:** Todas compartilham as mesmas conexões.

O que cada Thread tem de único:
- **Stack:** Cada thread tem sua própria pilha. Isso é crucial. A pilha armazena as variáveis locais e o histórico de chamadas de funções. 
- **Registradores:** Para salvar o contexto dela.
- **Estado:** Assim como um processo, a thread pode estar `Running`, `Ready` ou `Blocked`. 

---
### **3. Thread vs Processo**

| **Característica**    | **Processo**                                   | **Thread**                                                   |
| --------------------- | ---------------------------------------------- | ------------------------------------------------------------ |
| **Definição**         | Um programa em execução.                       | Uma unidade de execução _dentro_ de um processo.             |
| **Isolamento**        | **Total.** Processos não compartilham memória. | **Parcial.** Threads compartilham a memória do processo-pai. |
| **Custo de Criação**  | **Alto** (pesado).                             | **Baixo** (leve).                                            |
| **Troca de Contexto** | **Lenta e Cara.**                              | **Rápida e Barata.**                                         |
| **Compartilha**       | Nada (por padrão).                             | Memória (Heap, Code, Data) e Recursos (Arquivos).            |
| **Tem de Próprio**    | Tudo (Memória, Stack, Recursos...).            | Stack e Registradores.                                       |
| **Analogia**          | O canteiro de obras.                           | Um trabalhador _no_ canteiro.                                |

---
### **4. Exemplo: Thread por cliente**

1. **O Processo do Servidor**
    - Você inicia seu servidor. O Sistema Operacional (SO) cria **um Processo** para ele.
    - Esse processo é "pesado": ele recebe seu próprio espaço de memória isolado, suas permissões de segurança, etc.
    - Esse processo começa, por padrão, com **uma Thread** (a thread principal).
        
2. **A Thread Principal**
    - A sua thread principal é a que executa o `loop`. A função dela é uma só: ficar "bloqueada" (Waiting) na instrução `accept()`, esperando um novo cliente bater à porta.
        
3. **Chega o Cliente**
    - Quando o Cliente 1 se conecta, a thread principal "desbloqueia".
    - Ela executa a próxima instrução: "alocar uma thread para lidar com o cliente".
    - O seu processo agora cria uma **nova Thread (Thread 2)**.
    - Essa Thread 2 é "leve". Ela vive _dentro_ do espaço de memória do processo principal. Ela compartilha o `Heap` e os `Dados Globais`, mas ganha sua própria Stack privada.
    - A Thread 2 agora assume a comunicação com o Cliente 1.
    - A Thread principal volta imediatamente para o `loop` e fica "bloqueada" em `accept()` de novo, esperando o Cliente 2.
        
4. **Mapeando para o meu Hardware (AMD 8C/16T)**
    - O SO vê **16 núcleos lógicos** (graças ao SMT) disponíveis para agendar tarefas.
        
    - **8 Clientes:** O seu processo de servidor agora tem 9 threads (1 principal + 8 de clientes). O SO vai agendar essas 9 threads.
        
    - **Paralelismo Real:** Se todas as 8 threads de clientes precisarem fazer um cálculo _exatamente ao mesmo tempo_, seu computador é capaz de executar todas elas em **paralelismo real**, usando 8 núcleos físicos. O desempenho será fantástico.
        
5.  **O que Acontece com 100 Usuários Simultâneos**: Aqui é onde vemos a diferença entre **Paralelismo** (hardware) e **Concorrência** (software).
	
	- **Criação das Threads:** O seu processo de servidor vai, de fato, criar 101 threads. Elas existirão todas ao mesmo tempo dentro do seu processo. O SO agora tem 101 threads, mas apenas 16 "slots" para executá-las. 
	    
	- **Concorrência:** O SO vai dar a _ilusão_ de que todas as 101 threads estão rodando ao mesmo tempo. Ele fará isso da seguinte forma:
	    - Ele pega 16 das 101 threads e as coloca para rodar nos núcleos lógicos.
	    - Depois de uma fração de segundo, ele **pausa** essas 16 threads (salva o estado delas)  
	    - Ele então **carrega** outras 16 threads que estavam na fila ("Ready") e as deixa rodar
	    - Ele repete isso milhares de vezes por segundo.
	        
6. **O Limite Real desse Modelo:** Este é o verdadeiro problema do modelo "thread-por-cliente".
	- Cada thread, por mais "leve" que seja, exige sua própria pilha (Stack). O SO reserva um espaço de memória para essa pilha (por padrão, algo entre 1MB e 8MB).
	- **100 threads:** 100 * 1MB = 100MB de RAM (só para as pilhas). Fácil.
	- **10.000 threads:** 10.000 * 1MB = 10.000MB (ou 10GB) de RAM.	    
	- **O que acontece:** O seu sistema quebra por **falta de RAM** muito antes de a sua CPU se tornar o gargalo.
    