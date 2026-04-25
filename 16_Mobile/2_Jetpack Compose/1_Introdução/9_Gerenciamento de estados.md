
#Concluded 

----
#### **1. Recomposition** 

A recomposição é o processo de reexecução de uma função Composable. Ocorre sempre que um estado observado por uma função muda. Quando o estado varia, a função é chamada novamente para atualizar os elementos visuais e refletir o valor atual.

---
#### **2. Composable Stateful e stateless**

Um componente é considerado Stateful quando ele possui e gerencia seu próprio estado interno. 

Um componente é Stateless quando ele não mantém nenhum estado interno. Em vez de gerenciar variáveis, ele recebe seu estado atual por meio de parâmetros e comunica mudanças através de eventos para quem o chamou.

---
#### **3. State Hoisting**

O State Hoisting ocorre quando o estado de um componente é movido para a função que o chama. Esse processo transforma um componente que originalmente gerenciava seu próprio estado (**Stateful**) em um componente que apenas recebe dados e comunica eventos (**Stateless**).

Geralmente, o State Hoisting envolve a substituição de uma variável de estado interna por dois parâmetros:
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

---
#### **4. Salvando dados de UI**

O sistema Android pode destruir uma Activity e reiniciar o processo por dois motivos principais:
- **Mudanças de Configuração:** O exemplo mais comum é a rotação da tela e tema.
- **Morte do Processo:** Ocorre quando o sistema operacional encerra o aplicativo.

Sem os mecanismos de salvamento, campos de texto seriam limpos e a posição de listas seria reiniciada, gerando uma experiência negativa para o usuário.
- O **remember** mantém o estado apenas durante a recomposição.
- O **rememberSaveable** mantém o estado durante recomposição, rotação e morte do processo. Ele utiliza internamente um mecanismo chamado **Bundle**. O **Bundle** salva somente tipos primitivos.    

**Boas Práticas e Limitações**:
- Recomenda-se salvar apenas o estado essencial relacionado à entrada do usuário (texto digitado) e navegação (posição de rolagem).
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

---
#### **5. Ciclo de vida activity**

O ciclo de vida de uma Activity é um conjunto de estados pelos quais a tela do aplicativo passa, desde o momento em que é lançada até ser destruída 

- **onCreate()**:Aqui você deve realizar as inicializações estáticas, como inflar o layout, inicializar ViewModels e vincular dados a listas. Ele recebe um objeto **Bundle** que pode conter o estado anterior da UI para restauração.
    
- **onStart()**: Torna a Activity visível para o usuário. É o momento ideal para inicializar códigos que mantêm a interface atualizada.
    
- **onResume()**: A Activity entra em primeiro plano e torna-se interativa. Neste estado, você deve ativar componentes que precisam de foco exclusivo, como a câmera ou sensores (GPS).
    
- **onPause()**: É o primeiro sinal de que o usuário está saindo da tela, embora ela ainda possa estar parcialmente visível. Deve-se pausar operações que não devem continuar sem o foco do usuário.
    
- **onStop()**: A Activity não está mais visível para o usuário. É o ponto correto para liberar recursos intensivos e salvar dados persistentes no banco de dados.
    
- **onRestart()**: Chamado quando a Activity estava no estado _Stopped_ e o usuário volta para ela. Após este método, o sistema sempre chama o onStart().
    
- **onDestroy()**: A etapa final antes da destruição total da Activity. Ocorre quando o usuário termina a atividade ou o sistema a destrói para liberar memória.

Para otimizar o desempenho, siga estas diretrizes de implementação:
- **Recursos Interativos (Câmera, GPS)**: Devem ser iniciados no `onResume()` e liberados no `onPause()`. Isso garante que o recurso só esteja ativo enquanto o usuário interage diretamente com a tela, economizando bateria.
    
- **Recursos Visuais**: Podem ser iniciados no `onStart()` e liberados no `onStop()`. Isso é particularmente importante para suportar o modo **multi-janela**, onde sua Activity pode estar visível (no estado _Paused_), mas não ter o foco principal.


![400](../../../attachments/Pasted%20image%2020260408135237.png)
![](../../../attachments/Pasted%20image%2020260408135349.png)
