

----
#### **1. Recomposition** 

A recomposição é o processo de reexecução de uma função Composable. Ocorre sempre que um estado observado por uma função muda. Quando o dado (estado) varia, a função é chamada novamente para atualizar os elementos visuais e refletir o valor atual.

Variáveis locais comuns dentro de um Composable são recriadas a cada recomposição. Para que um valor persista entre essas execuções, utiliza-se a função `remember`, que armazena o objeto na memória durante a composição inicial e o mantém nas recomposições subsequentes.

---
#### **2. Composable Stateful e stateless**

Um componente é considerado Stateful quando ele possui e gerencia seu próprio estado interno. É útil em casos onde outros componentes não precisam acessar ou modificar esse dado específico.

Um componente é Stateless quando ele não mantém nenhum estado interno. Em vez de gerenciar variáveis, ele recebe seu estado atual por meio de parâmetros e comunica mudanças através de eventos (lambdas) para quem o chamou.

---
#### **3. State Hoisting**

O State Hoisting é um padrão de arquitetura no Jetpack Compose onde o estado de um componente é movido para a função que o chama. Esse processo transforma um componente que originalmente gerenciava seu próprio estado (**Stateful**) em um componente que apenas recebe dados e comunica eventos (**Stateless**).

Geralmente, o State Hoisting envolve a substituição de uma variável de estado interna por dois parâmetros principais:
- **value (T):** O valor atual que deve ser exibido na interface.
- **onValueChange: (T) -> Unit:** Uma função lambda que representa um evento, solicitando a alteração do valor quando o usuário interage com o componente.

```kotlin
// Componente Stateful
@Composable
fun HelloScreen() {
    var name by rememberSaveable { mutableStateOf("") }

    // O estado é "içado" para este componente
    HelloContent(
        name = name, 
        onNameChange = { name = it }
    )
}

// Componente Stateless
@Composable
fun HelloContent(name: String, onNameChange: (String) -> Unit) {
    Column(modifier = Modifier.padding(16.dp)) {
        Text(
            text = "Hello, $name",
            modifier = Modifier.padding(bottom = 8.dp),
            style = MaterialTheme.typography.bodyMedium
        )

        OutlinedTextField(
            value = name, 
            onValueChange = onNameChange, 
            label = { Text("Name") }
        )
    }
}
```

Neste exemplo, o componente HelloContent é altamente reutilizável e testável, ele apenas recebe uma String e notifica quando uma nova entrada ocorre.

---
#### **4. Salvando dados de UI**

O sistema Android pode destruir uma Activity e reiniciar o processo por dois motivos principais:
- **Mudanças de Configuração:** O exemplo mais comum é a rotação da tela e tema.
- **Morte do Processo:** Ocorre quando o sistema operacional encerra o aplicativo em segundo plano para liberar memória para outros processos com maior prioridade.

Sem os mecanismos de salvamento, campos de texto seriam limpos e a posição de listas seria reiniciada, gerando uma experiência negativa para o usuário.
- O **remember** mantém o estado apenas durante a recomposição; se a Activity for recriada, o valor é perdido.
- O **rememberSaveable** mantém o estado durante recomposição, rotação e morte do processo. Ele utiliza internamente um mecanismo chamado **Bundle**.

O **Bundle** salva tipos primitivos. Para objetos complexos, é necessário usar:
- **@Parcelize:** Para transformar objetos em parceláveis.
- **mapSaver ou listSaver:** APIs específicas do Compose para converter objetos em formatos que o Bundle aceite.      

**Boas Práticas e Limitações**:
- Recomenda-se salvar apenas o estado essencial relacionado à entrada do usuário (texto digitado) e navegação (posição de rolagem).
- O **Bundle** possui um tamanho limitado. Armazenar objetos grandes ou listas complexas pode causar a exceção **TransactionTooLargeException**.
- Para dados pesados, a boa prática é salvar apenas IDs ou chaves simples no **rememberSaveable** e recarregar os dados complexos da camada de persistência.


```kotlin
@Composable
fun ChatBubble(message: Message) {
    var showDetails by rememberSaveable { mutableStateOf(false) }

    Column {
        Text(
            text = message.content,
            modifier = Modifier.clickable { 
                showDetails = !showDetails // Altera o estado ao clicar
            }
        )
        
        // A UI reflete o estado salvo
        if (showDetails) {
            Text(text = message.timestamp)
        }
    }
}
```



O ciclo de vida de uma **Activity** no Android é um conjunto de estados pelos quais a tela do aplicativo passa, desde o momento em que é lançada até ser destruída pelo sistema ou pelo usuário. Compreender esse fluxo é essencial para gerenciar recursos corretamente e evitar problemas como travamentos, consumo excessivo de bateria ou perda de dados.

Abaixo, detalho os métodos fundamentais e o fluxo de transição entre eles:

### Os Principais Métodos do Ciclo de Vida

- **`onCreate()`**: É o primeiro método chamado quando a Activity é criada. Aqui você deve realizar as inicializações estáticas, como inflar o layout, inicializar ViewModels e vincular dados a listas. Ele recebe um objeto `Bundle` (chamado `savedInstanceState`) que pode conter o estado anterior da UI para restauração.
    
- **`onStart()`**: Torna a Activity visível para o usuário. É o momento ideal para inicializar códigos que mantêm a interface atualizada.
    
- **`onResume()`**: A Activity entra em primeiro plano e torna-se interativa. Neste estado, você deve ativar componentes que precisam de foco exclusivo, como a câmera ou sensores (GPS).
    
- **`onPause()`**: É o primeiro sinal de que o usuário está saindo da tela, embora ela ainda possa estar parcialmente visível. Deve-se pausar operações que não devem continuar sem o foco do usuário, mas **não** se deve salvar dados pesados neste método.
    
- **`onStop()`**: A Activity não está mais visível para o usuário. É o ponto correto para liberar recursos intensivos e salvar dados persistentes no banco de dados para evitar perda de informações.
    
- **`onRestart()`**: Chamado quando a Activity estava no estado _Stopped_ e o usuário volta para ela. Após este método, o sistema sempre chama o `onStart()`.
    
- **`onDestroy()`**: A etapa final antes da destruição total da Activity. Ocorre quando o usuário termina a atividade (clica em voltar) ou o sistema a destrói para liberar memória.
    

---

### Motivos para a Destruição da Activity

Existem dois cenários principais onde a Activity é encerrada:

1. **Destruição Natural**: Quando o usuário pressiona o botão "Voltar" ou o código executa explicitamente o método `finish()`. Nesse caso, o estado é perdido intencionalmente.
    
2. **Destruição pelo Sistema**: Ocorre devido a mudanças de configuração (como a rotação da tela) ou pressão de memória (quando o sistema precisa de recursos para outros apps). Aqui, o estado **precisa** ser salvo e restaurado para garantir uma boa experiência ao usuário.
    

---

### Gerenciamento Estratégico de Recursos

Para otimizar o desempenho, siga estas diretrizes de implementação:

- **Recursos Interativos (Câmera, GPS)**: Devem ser iniciados no `onResume()` e liberados no `onPause()`. Isso garante que o recurso só esteja ativo enquanto o usuário interage diretamente com a tela, economizando bateria.
    
- **Recursos Visuais**: Podem ser iniciados no `onStart()` e liberados no `onStop()`. Isso é particularmente importante para suportar o modo **multi-janela**, onde sua Activity pode estar visível (no estado _Paused_), mas não ter o foco principal.
    
- **Separação de Lógica**: Uma boa prática é não sobrecarregar os callbacks da Activity com lógica complexa. Utilize componentes cientes do ciclo de vida (_Lifecycle-Aware Components_) e o padrão **ViewModel** para manter o código limpo e os dados seguros durante as transições de estado.