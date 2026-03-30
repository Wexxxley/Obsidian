

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

### **2. Flow, LiveData e StateFlow**

Essas formas de comunicaçao entregam dados  da viewModel à UI do Compose.

**LiveData**: é uma classe de detentor de dados observável que é **ciente do ciclo de vida** (_lifecycle-aware_). Ele foi projetado especificamente para a camada de interface (UI).

- **Gerenciamento de Ciclo de Vida:** O `LiveData` respeita o ciclo de vida de outros componentes do app, como Activities e Fragments. Isso garante que o observador só receba atualizações quando o componente estiver em um estado ativo (`STARTED` ou `RESUMED`).
    
- **Segurança de Memória:** Como ele é ciente do ciclo de vida, o `LiveData` limpa automaticamente seus observadores quando o ciclo de vida associado é destruído (`DESTROYED`), evitando vazamentos de memória (_memory leaks_).
    
- **Thread Principal:** Por padrão, o `LiveData` entrega notificações na _Main Thread_. Para atualizar o valor a partir de uma thread de background, utiliza-se o método `postValue()`, enquanto `setValue()` é restrito à thread principal.
    
- **Limitação Técnica:** Ele opera apenas na camada de UI e não oferece operadores complexos de transformação de dados (como mapeamentos ou filtros avançados) de forma nativa e eficiente como as Coroutines.
    

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

