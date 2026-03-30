

---
O Room é uma camada de abstração (ORM - Object-Relational Mapping) sobre o SQLite. Ele mapeia objetos Kotlin diretamente para tabelas do banco.

![550](../../attachments/Pasted%20image%2020260330144101.png)

A arquitetura moderna do Android não permite que a UI fale diretamente com o database. Existe uma hierarquia lógica:

1. **Room (Database):** Armazena os dados localmente.
2. **Repository:** Atua como o mediador entre diferentes fontes de dados. Se o celular estiver offline, ele busca no Room. Se online, pode buscar na API e atualizar o Room.
3. **ViewModel:** Prepara o que a UI deve exibir.
4. **Flow / LiveData:** Os canais de comunicação que levam os dados do banco até a tela automaticamente.

### **1. ViewModel**

Ele busca os dados no Repositório e os expõe para a UI, garantindo que o app não precise consultar o banco de dados novamente após um simples giro de tela.

No Android, quando você gira a tela, a Activity é destruída e recriada. O ViewModel permanece na memória enquanto o usuário está naquela tela, independentemente de rotações.

### **2. LiveData e StateFlow**

Essas formas de comunicaçao entregam dados da viewModel à UI do Compose.

**LiveData**
O LiveData foi criado especificamente para o Android. Ele é um Container que só entrega os dados se o componente estiver ativo
- **Consciência de Ciclo de Vida:** Ele sabe se a sua `Activity` ou `Fragment` está aberta. Se o app for para o segundo plano, o `LiveData` para de enviar atualizações.
- **Foco em UI Tradicional:** Ele funciona perfeitamente com os layouts antigos.

**StateFlow**
O StateFlow faz parte da linguagem Kotlin. Ele é como um "cano de água" que está sempre cheio; se você abrir a torneira, a água sai na hora.

- **Sempre tem um valor:** Ao contrário do `LiveData`, o `StateFlow` te obriga a ter um valor inicial. Você nunca começa com o estado "vazio".
    
- **Poder das Coroutines:** Ele é feito para trabalhar com `viewModelScope.launch`. Isso permite usar ferramentas poderosas para filtrar, transformar ou combinar dados de várias fontes (API + Banco de Dados) facilmente.
    
- **Multiplataforma:** Como é código Kotlin puro, você pode usar a mesma lógica no Android, no iOS ou no Desktop.
    

### 3. As Diferenças Cruciais (Direto ao ponto)

- **Ciclo de Vida:** O `LiveData` se limpa sozinho quando a tela fecha. No `StateFlow`, você precisa dizer ao código para "parar de ouvir" quando a tela fechar (embora o Compose facilite muito isso).
    
- **Valor Inicial:** `StateFlow` exige um valor (ex: `0`). `LiveData` pode começar nulo.
    
- **Fluxo "Quente":** O `StateFlow` está sempre ativo. Se alguém novo começar a observar agora, ele recebe imediatamente a última foto do que aconteceu.
    

### 4. Qual escolher? (A Regra de Ouro)

Para não ter erro na hora de decidir, siga este guia:

- **Use LiveData se:** Você está trabalhando em um projeto mais antigo, que usa Java ou layouts em XML, e quer algo que gerencie o ciclo de vida do Android sem esforço.
    
- **Use StateFlow se:** Você está usando **Jetpack Compose** e **Kotlin**. É o padrão moderno, mais rápido e feito sob medida para a reatividade do Compose.
    

### Resumo da Lógica de Uso

No desenvolvimento moderno (2026), a tendência é que o `StateFlow` substitua o `LiveData` em quase tudo. Se você está aprendendo Compose agora, foque 100% em entender o `StateFlow`, pois ele é a base de como os dados fluem nas telas modernas.

Ficou mais claro agora o papel de cada um no seu código? Se precisar, posso mostrar um código lado a lado de como um `Switch` atualiza um `LiveData` versus um `StateFlow`. 

### 2. Kotlin Flow

O `Flow` faz parte da biblioteca de Coroutines do Kotlin e é um **fluxo de dados frio** (_cold stream_). Ele é utilizado para processar fluxos de dados de forma assíncrona.

- **Cold Stream (Fluxo Frio):** O código dentro de um construtor `flow { ... }` não é executado até que o fluxo seja coletado (`collect`). Isso significa que ele não consome recursos ou processamento enquanto não houver um receptor ativo.
    
- **Suspensão e Concorrência:** O `Flow` utiliza funções suspensas para emitir e coletar valores, o que permite realizar operações de I/O (como consultas ao banco de dados Room ou chamadas de API) sem bloquear a thread atual.
    
- **Operadores de Transformação:** Oferece uma vasta gama de operadores como `map`, `filter`, `zip` e `combine`, permitindo o processamento complexo de dados antes que eles cheguem à interface.
    
- **Independência de UI:** Ao contrário do `LiveData`, o `Flow` não possui conhecimento nativo do ciclo de vida do Android, funcionando em qualquer camada do sistema (Data, Domain ou UI).
    

### 3. StateFlow

O `StateFlow` é uma especialização do `SharedFlow` e funciona como um **fluxo de dados quente** (_hot stream_) que emite atualizações de estado. No Jetpack Compose, ele é o substituto moderno para o `LiveData`.

- **Hot Stream (Fluxo Quente):** Diferente do `Flow` comum, o `StateFlow` existe independentemente de ter coletores ativos. Ele sempre mantém um valor em memória.
    
- **Retenção de Estado:** Ele armazena o **último valor emitido**. Quando um novo coletor começa a observar o `StateFlow`, ele recebe imediatamente o estado atual.
    
- **Conformidade com Compose:** Através do método `collectAsStateWithLifecycle()`, o Compose consegue observar o `StateFlow` e disparar a recomposição da interface apenas quando o valor armazenado for alterado.
    
- **Unicidade de Valor:** O `StateFlow` não emite valores repetidos consecutivamente. Se você tentar atualizar o estado com um valor idêntico ao atual, os coletores não serão notificados (comportamento de `distinctUntilChanged`).

