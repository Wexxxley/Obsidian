

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
O StateFlow faz parte da linguagem Kotlin. É um fluxo de dados que retém permanentemente o último valor emitido em memória, enviando-o imediatamente a qualquer novo coletor que inicie a observação.
- **Sempre tem um valor:** Ao contrário do `LiveData`, o `StateFlow` te obriga a ter um valor inicial. Você nunca começa com o estado "vazio".
- **Coroutines:** Isso permite usar ferramentas poderosas para filtrar, transformar ou combinar dados de várias fontes (API + Banco de Dados) facilmente.
- **Multiplataforma:** Como é código Kotlin puro, você pode usar a mesma lógica no Android, no iOS ou no Desktop.

**Diferenças**
- O `LiveData` se limpa sozinho quando a tela fecha. No `StateFlow`, você precisa dizer ao código para "parar de ouvir" quando a tela fechar.
- O`StateFlow` exige um valor. `LiveData` pode começar nulo.
- O `StateFlow` está sempre ativo. Se alguém novo começar a observar agora, ele recebe imediatamente a última foto do que aconteceu.

