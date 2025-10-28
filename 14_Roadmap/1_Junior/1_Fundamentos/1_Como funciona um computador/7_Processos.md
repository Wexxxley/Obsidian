
#Concluded 

---
### 1. O que é um Processo? (Definição Técnica)

Um processo é uma **instância de um programa em execução**.

- Quando você clica duas vezes no ícone do Chrome, o arquivo `chrome.exe` (que está no seu SSD) é carregado na memória RAM. Esse "programa vivo" na RAM é um processo.
    
- Ele é uma entidade **ativa** e **isolada**. O sistema operacional (SO) garante que um processo não possa, por acidente ou malícia, acessar a memória de outro processo.

---
### 2. A Anatomia de um Processo

Para um processo existir, o SO aloca várias coisas para ele. Tudo isso fica guardado em uma estrutura de dados chamada **PCB (Process Control Block)**:

1. **Espaço de Endereçamento (Memória Virtual):** O processo acha que tem a memória RAM toda para ele (uma ilusão criada pelo SO). Esse espaço é dividido em:
    
    - **Code Segment:** Onde ficam as instruções do programa (o código binário).
    - **Data Segment:** Onde ficam as variáveis globais e estáticas.
    - **Heap:** Uma área de memória dinâmica, que cresce conforme o programa pede mais memória (ex: quando você abre uma nova aba no navegador).
    - **Stack:** Uma área crucial para guardar variáveis locais de funções e controlar a execução (quem chamou quem).
        
2. **Recursos do SO:**
    - **File Descriptors:** Uma lista de todos os arquivos que o processo abriu.
    - **Handles:** Conexões com outros recursos, como janelas na tela, conexões de rede (sockets), etc.
        
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

Como sua CPU só pode rodar um processo por vez (por núcleo), o SO precisa trocar quem está usando a CPU milhares de vezes por segundo para dar a ilusão de multitarefa. Isso se chama **Context Switch**.

Trocar de um processo para outro é "caro" computacionalmente. O SO precisa salvar _tudo_ do Processo A (registradores da CPU, ponteiros de memória, etc.) e carregar _tudo_ do Processo B. É como ter que desmontar todo o canteiro de obras e montar outro em milissegundos.