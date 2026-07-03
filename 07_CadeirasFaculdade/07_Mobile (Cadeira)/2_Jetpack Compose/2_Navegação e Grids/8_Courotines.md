

---
Por padrão todos os componentes de um aplicativo Android são executados na mesma Thread, a Main Thread. Ela é a única responsável pelas atualizações da interface com o usuário. Se a main thread for bloqueada, pode ocasionar o aparecimento do famoso ANR (Aplicativo Não Respondendo).

As vezes multi-thread é necessário, como:
- Leitura escrita no db;
- Chamadas a APIS.
- Executar várias tarefas simultaneamente sem bloqueio

**Courotines**: Diferentmente de thread que são gerenciadas pelo sistema operacional coroutines são gerenciadas pelo usuário, so que com bem mais legibilidade.

Em kotlin são funções que possuem:
- suspend: Pausa a execução de uma coroutine, salvando as variáveis locais.
- resume: Continua a execução de uma coroutine que está suspensa.

![](../../../../attachments/Pasted%20image%2020260602132529.png)

- **Coroutine Builder:** São funções que iniciam uma nova corrotina. 
- **Dispatcher:** Define em qual thread a corrotina será executada. 
- **Job:** É o identificador da corrotina. Quando você chama `launch`, ele retorna um `Job`, que permite controlar o ciclo de vida dessa tarefa.
- **Suspend Function:** São funções marcadas com o modificador `suspend`. Elas podem pausar a execução da corrotina sem bloquear a thread onde ela está rodando, permitindo que a thread execute outras tarefas enquanto.
- **Await:** É uma função chamada em um `Deferred` (retornado pelo `async`). Ela suspende a corrotina atual até que o resultado da operação assíncrona esteja pronto. 

![](../../../../attachments/Pasted%20image%2020260602132814.png)
- Você só pode chamar uma função suspend de dentro de outra função suspend ou de dentro de um Coroutine Scope.
- Quando o escopo é cancelado, todas as Coroutines lançadas dentro dele são automaticamente cancelada

**CourotineBuilders**
- **launch**: Inicia uma nova coroutine sem bloquear a thread atual. Usado quando quando não precisamos esperar o resultado.
- **async**: Inicia uma coroutine e permite esperar por seu resultado para continuar. Usamos função await para suspender o código até recuperar o resultado. Retorna um Deffered que é uma subclasse de Job.
- **runBlocking**: Bloqueia a thread em que é chamado enquanto a coroutine não terminar. 

**Dispatchers**
![](../../../../attachments/Pasted%20image%2020260602133956.png)


**withContext**: Permite que você execute uma parte específica do seu código em um Dispatcher diferente daquele que está sendo usado pelo escopo principal, sem a necessidade de iniciar uma nova corrotina.

![](../../../../attachments/Pasted%20image%2020260602140630.png)

**viewModelScope**
É um CoroutineScope que está disponível automaticamente em todo ViewModel. Qualquer Coroutine lançada no viewModelScope será automaticamente cancelada quando o ViewModel for limpo 

![](../../../../attachments/Pasted%20image%2020260602141505.png)


**Funções suspend devem ser chamadas na Thread Principal**

**Injeção de Dependência de Dispatchers**
- Nunca utilize Dispatchers "hardcoded" dentro do corpo da função, como `Dispatchers.Default` ou `Dispatchers.IO`. Em vez disso, injete-os através do construtor da classe.

**ViewModel como Gestor de Corrotinas**
- A camada de UI (Jetpack Compose) deve ser declarativa e ignorante sobre a lógica de negócios.  A lógica deve ser iniciada no `ViewModel`. O `ViewModel` possui escopos de corrotinas específicos, como o `viewModelScope`.

**Fique atento às exceções**
- Exceções não tratadas em coroutines podem causar a falha do seu aplicativo.