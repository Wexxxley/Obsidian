
#Concluded 

----
#### **1. Recomposition** 

A recomposição é o processo de reexecução de uma função Composable. Ocorre sempre que um estado observado por uma função muda. Quando o estado varia, a função é chamada novamente para atualizar os elementos visuais e refletir o valor atual.

#### **2. Composable Stateful e stateless**

- Um componente é considerado Stateful quando ele possui e gerencia seu próprio estado interno. 

- Um componente é Stateless quando ele não mantém nenhum estado interno. Em vez de gerenciar variáveis, ele recebe seu estado atual por meio de parâmetros e comunica mudanças através de eventos para quem o chamou.

#### **3. State Hoisting**

O State Hoisting ocorre quando o estado de um componente é movido para a função que o chama. Esse processo transforma um componente que originalmente gerenciava seu próprio estado (**Stateful**) em um componente que apenas recebe dados e comunica eventos (**Stateless**).

Nesse exemplo seria interessante fazer o hoisting do estado
![520](../../../attachments/Pasted%20image%2020260428143232.png)

Depois do hoisting
![550](../../../attachments/Pasted%20image%2020260428144224.png)

Atualizando para vários produtos
![570](../../../attachments/Pasted%20image%2020260428145253.png)
![550](../../../attachments/Pasted%20image%2020260428145527.png)

#### **4. Salvando dados de UI**

O sistema Android pode destruir uma Activity e reiniciar o processo por dois motivos principais:
- **Mudanças de Configuração:** rotação da tela, mudança de tema, estilo etc.
- **Morte do Processo:** como ao fechar o app.

Sem os mecanismos de salvamento, campos de texto seriam limpos e a posição de listas seria reiniciada.
- O **rememberSaveable** mantém o estado durante recomposição, rotação e morte do processo. Ele utiliza internamente um mecanismo chamado **Bundle**. 

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