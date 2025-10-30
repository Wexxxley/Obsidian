
#Concluded 

---
### 1. O que é um Processo? (Definição Técnica)

Um processo é uma<mark style="background: #ADCCFFA6;"> instância de um programa em execução.</mark>

- Quando você clica duas vezes no ícone do Chrome, o arquivo `chrome.exe` (que está no SSD) é carregado na RAM. <mark style="background: #ADCCFFA6;">Esse "programa vivo" na RAM é um processo.</mark>
    
- Ele é uma entidade **ativa** e **isolada**. O sistema operacional (SO) garante que um processo não possa, por acidente ou malícia, acessar a memória de outro processo.

---
### 2. A Anatomia de um Processo

Para um processo existir, o <mark style="background: #ADCCFFA6;">SO aloca várias coisas para ele. Tudo isso fica guardado em uma estrutura de dados chamada PCB (Process Control Block):</mark>

1. **Memória Virtual:** O processo acha que tem a memória RAM toda para ele (uma ilusão criada pelo SO). Esse espaço é dividido em:
    - **Code Segment:** Onde ficam as instruções (código binário).
    - **Data Segment:** Onde ficam as variáveis globais e estáticas.
    - **Heap:** Uma área de memória dinâmica, que cresce conforme o programa pede mais memória (ex: quando você abre uma nova aba no navegador).
    - **Stack:** Uma área crucial para guardar variáveis locais de funções e controlar a execução (quem chamou quem).
        
2. **Recursos do SO:**
    - **File Descriptors:** Uma lista de todos os arquivos que o processo abriu.
    - **Handles:** Conexões com outros recursos, como janelas na tela, conexões de rede, etc.
        
3. **Contexto de Segurança:**
    - Quem é o "dono" desse processo? (Usuário comum? Administrador?). Isso define o que ele pode ou não fazer.

---
### 3. O Ciclo de Vida de um Processo

- **New:** Está sendo criado pelo SO.
- **Ready:** Está na memória RAM, pronto para rodar, só esperando a CPU ficar livre.
- **Running:** A CPU está ativamente executando suas instruções agora. (Em um núcleo de CPU, apenas _um_ processo pode estar nesse estado por vez).
- **Waiting/Blocked:** Ele parou porque precisa de algo externo. Exemplo: o processo do Word fica "bloqueado" esperando você digitar uma tecla. Ele não gasta CPU enquanto espera.
- **Terminated:** Acabou o trabalho e o SO está limpando a bagunça que ele deixou na RAM.

---
### 4. Context Switch - O Custo do Processo

Como sua CPU só pode rodar um processo por vez (por núcleo), o <mark style="background: #ADCCFFA6;">SO precisa trocar quem está usando a CPU milhares de vezes por segundo para dar a ilusão de multitarefa. Isso se chama Context Switch.</mark>

Trocar de um processo para outro é "caro" computacionalmente. O SO precisa salvar _tudo_ do Processo A (registradores da CPU, ponteiros de memória, etc.) e carregar _tudo_ do Processo B. É como ter que desmontar todo o canteiro de obras e montar outro em milissegundos.


---
### **5. Stack vs Heap**

Ambos **Stack** (pilha )e **Heap** (pilha de alocação) são apenas **regiões da memória RAM** que o seu processo usa. Mas a _forma_ como eles são usados e gerenciados é completamente diferente.

#### **5.1 Stack (Pilha)**
A Stack é uma região de memória altamente organizada, usada para armazenar dados de escopo local. Ela funciona como uma pilha de pratos.


- **Como funciona:** Quando você chama uma função (ex: calcularMedia(a, b)), o programa "empilha" um Stack Frame nessa pilha.
    
- **O Stack Frame possui:**
    - Os argumentos da função.
    - As variáveis locais declaradas _dentro_ da função.
    - Para onde a CPU deve pular de volta quando a função terminar.
        
- **Termino:** Quando a função termina, seu o Stack Frame é "desempilhado"  e todo o seu conteúdo é destruído.
    
- **Velocidade:** Isso é _extremamente_ rápido. O gerenciamento é feito apenas mudando um ponteiro de CPU (o "Stack Pointer") para cima ou para baixo.
    
- **Tamanho Fixo:** A Stack tem um tamanho fixo (definido quando o processo/thread é criado, geralmente 1MB a 8MB).
    
- **Stack Overflow**: Acontece quando você tenta "empilhar" mais coisas do que cabem na Stack. Por exemplo quand você usar **Recursão infinita**. 

#### **5.1 Heap (Pilha de Alocação)**

É um grande "depósito" desorganizado, usado para alocar dados de forma dinâmica, ou seja, dados que você não sabe o tamanho ou o tempo de vida quando está escrevendo o código.

- **Como funciona:**    
    1. **Alocação**: Você _pede_ ao SO/runtime: "Ei, preciso de 500 bytes de memória no Heap para guardar um objeto". (Ex: new no Java/C#)
    2. O SO procura um bloco de memória livre desse tamanho.
    3. Ele "aluga" esse bloco para você e te devolve um ponteiro.
    4. Esse ponteiro é armazenado em uma variável na sua **Stack**.
            
- **Velocidade:** A alocação no Heap é _muito mais lenta_ que na Stack.
    
- **O que vai para o Heap?**
	- **Objetos:** Em linguagens como Java e C#, _todos_ os objetos vão para o Heap.
	- **Dados de "Tempo de Vida Longo":** Qualquer dado que precise sobreviver _depois_ que a função que o criou terminar. Se estivesse na Stack, ele morreria. No Heap, ele vive até ser explicitamente destruído.
    
##### **5.1.1 Limitações e Problemas**

- **Gerenciamento Manual:** Você é responsável por "devolver" a memória quando não precisar mais (Ex: `delete` no C++)
    
- **Memory Leak**: Ocorre quando você aloca memória no Heap, e perde o ponteiro antes de devolver o espaço. O espaço fica "alugado" para sempre, inacessível. 
        
- ****Garbage Collector (Java, C#, Python):** Linguagens como java, cElas têm um **Garbage Collector (Coletor de Lixo)**, um processo de fundo que automaticamente encontra e libera memória do Heap que não está mais sendo usada, prevenindo a maioria dos vazamentos.
    
- **Problema 2: Fragmentação:** Com o tempo, o Heap fica parecendo um queijo suíço, cheio de pequenos blocos alugados e liberados. Pode ser difícil encontrar um bloco _contínuo_ grande o suficiente, mesmo que o total de memória livre seja alto.
    

---

### Resumo da Comparação (Stack vs. Heap)

|**Característica**|**Stack (Pilha)**|**Heap (Pilha de Alocação)**|
|---|---|---|
|**Gerenciamento**|**Automático** (pela CPU/Compilador)|**Manual** (pelo Programador) ou **Automático** (pelo Garbage Collector)|
|**Velocidade**|**Muito Rápida** (mudar um ponteiro)|**Lenta** (envolve busca/gerenciamento do SO)|
|**Estrutura**|Altamente organizada (LIFO)|Desorganizada (um "depósito")|
|**Tamanho**|**Pequeno e Fixo** (ex: 1MB)|**Grande e Dinâmico** (limitado pela RAM do sistema)|
|**O que armazena**|Variáveis locais, argumentos de função, ponteiros.|Objetos, dados dinâmicos, dados de vida longa.|
|**Problema Típico**|**Stack Overflow** (Estouro de Pilha)|**Memory Leak** (Vazamento de Memória) e **Fragmentação**|
|**No Contexto de Threads**|**Privada** (Cada thread tem sua _própria_ Stack)|**Compartilhado** (Todas as threads compartilham o _mesmo_ Heap)|