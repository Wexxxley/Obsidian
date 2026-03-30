

---
O Room é uma camada de abstração (ORM - Object-Relational Mapping) sobre o SQLite. Ele mapeia objetos Kotlin diretamente para tabelas do banco.

![550](../../attachments/Pasted%20image%2020260330144101.png)

A arquitetura moderna do Android não permite que a UI fale diretamente com o database. Existe uma hierarquia lógica:

1. **Room (Database):** Armazena os dados localmente.
    
2. **Repository (Repositório):** Atua como o mediador (controlador de tráfego) entre diferentes fontes de dados (Banco local vs. API na internet).
    
3. **ViewModel:** Protege os dados durante mudanças de configuração (como girar a tela) e prepara o que a UI deve exibir.
    
4. **Flow / LiveData:** Os canais de comunicação que levam os dados do banco até a tela automaticamente.
    

### 2. ViewModel: O Guardião do Ciclo de Vida

O principal problema resolvido pelo `ViewModel` é a perda de dados. No Android, quando você gira a tela, a `Activity` é destruída e recriada.

- **Funcionamento:** O `ViewModel` permanece na memória enquanto o usuário está naquela tela, independentemente de rotações.
    
- **Papel Lógico:** Ele busca os dados no Repositório e os expõe para a UI, garantindo que o app não precise consultar o banco de dados novamente após um simples giro de tela.
    

### 3. Flow, LiveData e StateFlow: Os Canais Reativos

Esses componentes permitem que a UI se atualize sozinha sempre que o banco de dados mudar.

|**Componente**|**Contexto de Uso**|**Características Principais**|
|---|---|---|
|**LiveData**|Projetos Java / XML|Ciclo de vida integrado; ideal para visualizações simples em XML.|
|**Flow**|Kotlin (Geral)|Funciona como um "rio" de dados; excelente para combinar múltiplas fontes (API + Banco).|
|**StateFlow**|**Jetpack Compose**|Versão moderna do LiveData para Kotlin; armazena o último estado e é altamente performático.|

### 4. Repository: O Controlador de Tráfego

O `Repository` resolve o problema do "código espaguete" (lógica misturada).

- **Centralização:** É uma classe que decide de onde os dados vêm. Se o celular estiver offline, ele busca no **Room**. Se estiver online, pode buscar na **API** e atualizar o Room.
    
- **Abstração:** A interface (UI) não precisa saber de onde o dado veio; ela apenas pede ao Repositório, que entrega a informação pronta.
    

### 5. Synergy (Sinergia): O Ciclo Completo

A aula descreve o caminho que a informação percorre em um app de alta performance:

1. **Room** guarda os dados (estratégia _offline-first_).
    
2. **Repository** gerencia a sincronização entre local e web.
    
3. **ViewModel** solicita os dados e os mantém seguros.
    
4. **StateFlow/Flow** entrega esses dados à UI do Compose em tempo real.
    

### Termos Técnicos Explicados

- **Lifecycle-aware (Ciente do ciclo de vida):** Componentes que sabem quando a tela está visível ou fechada, evitando vazamentos de memória e crashes.
    
- **Suspended Functions (Funções Suspensas):** Funções usadas no Room e Repository que podem ser pausadas sem travar a interface do usuário (essencial para operações pesadas de banco de dados).
    
- **collectAsState:** Método usado no Jetpack Compose para "ouvir" um `StateFlow` e transformar o fluxo de dados em um estado que a UI consegue desenhar.
    

Esta estrutura é o que permite que aplicativos como Spotify e X (Twitter) funcionem de forma fluida mesmo com conexões de internet instáveis.