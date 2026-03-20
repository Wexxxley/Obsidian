

---
A ferramenta toast fornece feedbacks rápidos e não intrusivos ao usuário. O Toast aparece como um pequeno pop-up que não interrompe a interação com a tela e desaparece automaticamente após alguns segundos.

- **Exemplos:** "E-mail enviado", "Download concluído" ou "Item salvo nos favoritos".

## 2. A Função `Toast.makeText()`

Para criar um Toast, utiliza-se o método estático `makeText`. Ele exige três parâmetros obrigatórios:

- **Context (Contexto):** Define em qual parte da aplicação o Toast está operando. No Jetpack Compose, obtemos o contexto atual através de `LocalContext.current`.
    
- **Text (Mensagem):** A String que será exibida para o usuário.
    
- **Duration (Duração):** Define por quanto tempo a mensagem ficará na tela. Existem duas constantes pré-definidas:
    
    - `Toast.LENGTH_SHORT`: Exibição por cerca de 2 segundos.
        
    - `Toast.LENGTH_LONG`: Exibição por cerca de 3.5 segundos.
        

## 3. O Papel do Contexto no Compose

Um ponto técnico crucial mencionado é que o `LocalContext.current` só pode ser acessado dentro de funções marcadas com a anotação `@Composable`.

- **Uso correto:** Você captura o contexto no início da sua função Composable e o utiliza dentro de lambdas de clique (como o `onClick` de um botão).
    

## 4. A Importância do Método `.show()`

Um erro comum de iniciantes é configurar o Toast e esquecer de exibi-lo. O `makeText()` apenas cria o objeto da mensagem; para que ela apareça fisicamente na tela do dispositivo, é obrigatório chamar o método `.show()` ao final da instrução.

## 5. Exemplo de Implementação Técnica

Abaixo, apresento o código unificado baseado na aula, estruturado de forma lógica:

Kotlin

```
@Composable
fun ExemploToast() {
    // 1. Obtendo o contexto da aplicação (obrigatório para Toasts)
    val contexto = LocalContext.current

    Column(
        modifier = Modifier.fillMaxSize(),
        verticalArrangement = Arrangement.Center,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Button(
            onClick = {
                // 2. Criando e exibindo o Toast imediatamente ao clicar
                Toast.makeText(
                    contexto,                         // Contexto
                    "Esta é uma mensagem Toast!",      // Mensagem
                    Toast.LENGTH_LONG                 // Duração
                ).show()                              // Comando para exibir
            }
        ) {
            Text(text = "Exibir Mensagem")
        }
    }
}
```

## 6. Resumo de Boas Práticas

- **Concisão:** Mantenha as mensagens curtas para que o usuário consiga ler rapidamente antes que desapareçam.
    
- **Localização:** Evite colocar informações críticas em Toasts, pois se o usuário desviar o olhar por 3 segundos, ele perderá a informação sem chance de recuperá-la.
    
- **Encadeamento:** É comum escrever a instrução em uma única linha: `Toast.makeText(...).show()`.
    

Deseja que eu explique como personalizar o posicionamento do Toast na tela ou como criar um Toast customizado com ícones?