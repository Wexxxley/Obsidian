

---

Biblioteca de navegação projetada para funcionar com o Compose
- O desenvolvedor tem total controle sobre a **backstack**.
- Navegar é tão simples quanto adicionar e remover itens de uma lista
- Fornece um sistema de navegação flexível ao prover: • Atualização automática da interface por meio de mudanças na backstack • Sistema de layout adaptável permite mostrar vários destinos ao mesmo tempo • Um mecanismo de comunicação entre layouts por meio de metadados

**BackStack**
O _BackStack_ é uma pilha de destinos (keys das telas) por onde o usuário passou. Ele funciona seguindo o princípio LIFO (_Last In, First Out_)

Embora a transição para rotas baseadas em objetos tenha mudado a forma como declaramos as rotas, o conceito de _BackStack_ permanece idêntico. Ele é responsável por:
1. **Gerenciamento de Ciclo de Vida:** Quando uma tela é empilhada, ela é criada. Quando ela é desempilhada (removida do _BackStack_), o sistema destrói o estado dessa tela e seu ViewModel associado.
2. **Controle de Fluxo (PopUpTo):** Você utiliza o _BackStack_ para manipular o histórico. Com o parâmetro `popUpTo`, você instrui o `NavController` a remover elementos da pilha até encontrar um destino específico, impedindo que o usuário retorne para fluxos que já foram finalizados.


![650](../../../attachments/Pasted%20image%2020260603084035.png)
- **val backStack**: O "BackStack" não é mais um objeto abstrato gerenciado pelo sistema, mas uma lista (`mutableStateListOf`) que você controla diretamente.
    - `Home` é o item inicial.
    - Ao adicionar um item (`backStack.add(...)`), você navega.
    - Ao remover um item (`backStack.removeLastOrNull()`), você volta.
        
- **NavDisplay**: Este é o componente que "observa" a lista backStack. Ele é o responsável por renderizar o conteúdo.
    - onBack: Define o comportamento de retorno, que neste caso é simplesmente remover o último item da lista.
        
- **entryProvider**: Fábrica de destinos. O NavDisplay chama essa função passando a key (o objeto que está no topo da pilha).
    - **when:** O código usa `when` para verificar qual o tipo do objeto na pilha.
    - **NavEntry(key)**: É o encapsulamento que mencionamos antes. Ele recebe a chave(o estado) e um bloco de conteúdo (o Composable que será exibido).

![](../../../attachments/Pasted%20image%2020260603084603.png)