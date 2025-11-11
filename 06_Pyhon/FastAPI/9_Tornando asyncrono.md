
---

Um dos problemas ao lidarmos com uma aplicação web é a necessidade de estarmos sempre disponíveis para responder a requisições enviadas pelos clientes. Quando recebemos uma requisição, normalmente precisamos processá-la: validar, conectar ao banco de dados, realizar algumas operações e, finalmente, retornar o recurso solicitado.

Em um cenário síncrono, enquanto processamos uma requisição, não conseguimos processar outra até que a primeira seja concluída. Esse fluxo de execução é chamado de blobueante, pois a aplicação fica "parada", aguardando a resposta de sistemas externos. Esse tempo de espera é conhecido como **bloqueio por I/O (Input/Output)** 

---
###  **1. Uvicorn não é bloqueante**

Quando dizemos que a aplicação está bloqueada, estamos nos referindo somente a aplicação. O servidor de aplicação, em nosso caso o uvicorn, já trabalha de forma não bloqueante. 

Além disso, ele pode inicializar diversas cópias da nossa aplicação (mesmo síncronas) em um formato de workers e executar diversos processos para nossa aplicação. Se quisermos inicializar o uvicorn nesse modo, a única alteração necessária seria adicionar a flag `--workers <int>`. Algo como: `uvicorn main:app --reload --workers 3`. Fazendo com que nossa aplicação seja "clonada" em três processos.

![Pasted image 20250626183431](../../attachments/Pasted%20image%2020250626183431.png)

- **Servidor**: O Uvicorn é o software que recebe as requisições HTTP dos clientes. Ele atua como uma interface entre a internet e sua aplicação Python.
- **Assíncrono:** O uvicorn é construído para lidar com múltiplas requisições concorrentemente, sem bloquear o processo principal. Isso é crucial para aplicações de alta performance que fazem muitas operações.
- Quando você executa o comando `uvicorn main:app --reload`, você está _iniciando_ o software Uvicorn nessa máquina.
- "backlog" é a **fila interna de requisições ou conexões pendentes** que o servidor não conseguiu processar imediatamente.

---
###  **2. Bloqueio de I/O**

Quando o código precisa interagir com sistemas externos ele fica "parado", aguardando a resposta para seguir com a execução. 

![Pasted image 20250626184626](../../attachments/Pasted%20image%2020250626184626.png)

---
### **3. Função assíncrona**

Função que pode ser suspensa em determinados pontos e retomar a execução mais tarde. Isso permite que a aplicação não fique "parada" enquanto espera por uma resposta, permitindo que o Python execute outras tarefas enquanto aguarda a conclusão da operação.

Em python, corrotinas são definidas com a palavra-chave `async`. O `await` é usado para chamar operações que podem levar algum tempo, pelo bloqueio de I/O. Isso permite que o Python "libere" o controle de volta para o loop de eventos que pode executar outras tarefas enquanto aguarda a operação.

---
### **4. Loop de eventos**

O loop de eventos é responsável por coordenar a execução das corrotinas. Em termos simples, o loop de eventos é um loop infinito que gerencia todas as corrotinas e garante que elas sejam executadas em ordem, permitindo o escalonamento de várias tarefas.

Todas as corrotinas são enviadas para o loop de eventos, no momento em que são chamadas. Essas corrotinas são executadas sequencialmente. No entanto, quando o loop encontra a palavra-chave `await`, ele a "deixa de lado" temporariamente, até que a tarefa que estava sendo aguardada termine. O loop então retoma a execução da próxima corrotina, ou a que estiver pronta para ser executada, até encontrar outro `await` e assim por diante.

![Pasted image 20250626190850](../../attachments/Pasted%20image%2020250626190850.png)

