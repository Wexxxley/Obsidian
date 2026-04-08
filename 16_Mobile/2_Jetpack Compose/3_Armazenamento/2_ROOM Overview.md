

---
O Room é uma camada de abstração (ORM - Object-Relational Mapping) sobre o SQLite. Ele mapeia objetos Kotlin diretamente para tabelas do banco.

![550](../../../attachments/Pasted%20image%2020260330144101.png)

A arquitetura moderna do Android não permite que a UI fale diretamente com o database. Existe uma hierarquia lógica:

1. **Room (Database):** Armazena os dados localmente.
2. **Repository:** 
3. **ViewModel:** Prepara o que a UI deve exibir.
4. **Flow / LiveData:** Os canais de comunicação que levam os dados do banco até a tela automaticamente.

### **1. DAO vs REPOSITORY** 

DAO É o nível mais baixo. Ele só entende de SQL. A função dele é converter comandos do banco de dados em objetos Kotlin. 

O Repository Atua como o mediador entre diferentes fontes de dados. Se o celular estiver offline, ele busca no Room. Se online, pode buscar na API e atualizar o Room.
### **2. ViewModel**

A ViewModel é o intermediário de estado entre a UI e os dados. Suas duas funções principais são:
1. **Sobrevivência ao Ciclo de Vida:** No Android, se você girar a tela, a sua Activity é destruída e recriada. Se os dados estivessem na tela, eles seriam apagados. A ViewModel permanece viva na memória, segurando os dados para que a tela os recupere instantaneamente ao "renascer".
    
2. **Preparação de Dados:** O Repositório entrega dados brutos. A ViewModel os transforma em algo que a UI consiga exibir facilmente. Por exemplo, o Repositório entrega uma lista de 100 notas, e a ViewModel filtra para mostrar apenas as notas "Favoritas" na tela.
### **2. LiveData e StateFlow**

Essas formas de comunicaçao entregam dados da viewModel à UI do Compose.

**LiveData**
O LiveData foi criado especificamente para o Android. Ele é um Container que só entrega os dados se o componente estiver ativo
- **Consciência de Ciclo de Vida:** Ele sabe se a sua `Activity`está aberta. Se o app for para o segundo plano, o `LiveData` para de enviar atualizações.
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

