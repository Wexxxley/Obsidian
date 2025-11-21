

---
## **1. Runtime Environment**

O **Node.js é um ambiente de execução (runtime) JavaScript** construído sobre a **engine V8** do Google Chrome. Ele permite a execução de código JavaScript fora do navegador. Ao contrário de plataformas baseadas em threads concorrentes (como servidores Java tradicionais), o Node.js opera sob um modelo de **I/O não bloqueante e orientado a eventos**.

**Libuv**: Biblioteca C que fornece suporte a operações de I/O assíncronas baseadas em eventos. Embora o JavaScript seja single-threaded, a Libuv mantém um pool de threads para executar operações pesadas de sistema operacional.

É crucial entender que o Node.js é **Single-Threaded** no que tange a execução do código JavaScript do usuário e o Event Loop. No entanto, o Node.js é **concorrente** através do Event Loop.

