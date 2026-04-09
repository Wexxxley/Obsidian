

---
O Room é uma camada de abstração (ORM - Object-Relational Mapping) sobre o SQLite. Ele mapeia objetos Kotlin diretamente para tabelas do banco.

![550](../../../attachments/Pasted%20image%2020260330144101.png)

A arquitetura moderna do Android não permite que a UI fale diretamente com o database. Existe uma hierarquia lógica:

1. **Room (Database):** Armazena os dados localmente.
2. **Repository**: repositório de acesso a dados de diversas fontes
3. **ViewModel:** Prepara o que a UI deve exibir.
4. **Flow / LiveData:** Os canais de comunicação que levam os dados até a tela.

### **1. DAO vs REPOSITORY** 

DAO É o nível mais baixo. Ele só entende de SQL. A função dele é converter comandos do banco de dados em objetos Kotlin. 

O Repository Atua como o mediador entre diferentes fontes de dados. Se o celular estiver offline, ele busca no Room. Se online, pode buscar na API e atualizar o Room.
### **2. ViewModel**

A ViewModel é o intermediário de estado entre a UI e os dados. Suas duas funções principais são:
1. **Sobrevivência ao Ciclo de Vida:** Se você girar a tela, a sua Activity é destruída e recriada. Se os dados estivessem na tela, eles seriam apagados. A ViewModel permanece viva na memória, segurando os dados para que a tela os recupere instantaneamente ao "renascer".
2. **Preparação de Dados:** O Repositório entrega dados brutos. A ViewModel os transforma em algo que a UI consiga exibir facilmente. Por exemplo, o Repositório entrega uma lista de 100 notas, e a ViewModel filtra para mostrar apenas as notas "Favoritas" na tela.
### **3. LiveData e StateFlow**

**LiveData**: Criado para Java e layouts em XML. Ele é "ciente do ciclo de vida". Ele para de enviar dados se a tela estiver fechada, evitando erros. No Jetpack Compose moderno, ele está sendo substituído.

**Flow**: É um fluxo frio. O Flow não armazena o último valor emitido. Se um novo coletor iniciar a observação, o fluxo recomeçará do início. Cada coletor aciona uma nova execução do bloco de código. Se houver dois coletores para um `Flow` que faz uma busca no banco de dados, a busca será realizada duas vezes de forma independente.

**Stateflow**: É um fluxo quente. Ele é a ferramenta padrão para expor dados da ViewModel para o Jetpack Compose. O StateFlow sempre armazena o último valor emitido em um buffer interno.
