

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


![650](../../../../attachments/Pasted%20image%2020260603084035.png)
- **val backStack**: O "BackStack" não é mais um objeto abstrato gerenciado pelo sistema, mas uma lista (`mutableStateListOf`) que você controla diretamente.
    - `Home` é o item inicial.
    - Ao adicionar um item (`backStack.add(...)`), você navega.
    - Ao remover um item (`backStack.removeLastOrNull()`), você volta.
        
- **NavDisplay**: Este é o componente que "observa" a lista backStack. Ele é o responsável por renderizar o conteúdo.
    - onBack: Define o comportamento de retorno, que neste caso é simplesmente remover o último item da lista.
        
- **entryProvider**: Fábrica de destinos. O NavDisplay chama essa função passando a key (o objeto que está no topo da pilha).
    - **when:** O código usa `when` para verificar qual o tipo do objeto na pilha.
    - **NavEntry(key)**: É o encapsulamento que mencionamos antes. Ele recebe a chave(o estado) e um bloco de conteúdo (o Composable que será exibido).

![](../../../../attachments/Pasted%20image%2020260603084603.png)

---

**Animações**

É possível substituir as animações padrão por meio parâmetros de transição ao NavDisplay
- **transitionSpec**: Define a animação ao navegar para frente. 
- **popTransitionSpec**: Define a animação ser aplicada quando o conteúdo é removido.QSa
- **predictivePopTransitionSpec**: Define a animação a ser aplicada quando o conteúdo é removido da pilha usando um gesto preditivo de volta

---
### Adaptive layouts

A grande variedade de dispositivos no ecossistema Android exige que o mesmo aplicativo se comporte de maneira adequada em diferentes configurações físicas de tela. 

- **Layouts responsivos** realizam pequenos ajustes na interface do usuário para otimizar o uso do espaço disponível.
- **Layouts adaptativos** executam mudanças estruturais na interface, como a transição de uma visualização de painel único para uma de painéis duplos.

A partir da API 36, o sistema operacional passa a ignorar diversas restrições definidas em código, tai como a fixação da orientação da tela. Devido a essas novas políticas do sistema, a interface do usuário pode sofrer alterações de tamanho a qualquer momento, e os aplicativos podem entrar em modo multijanela com mais frequência.

**Window Size Classes:** definem pontos de quebra exatos para categorizar o espaço disponível na interface.

- **Compact:** Largura inferior a 600dp. Representa a quase totalidade dos smartphones convencionais na orientação retrato.
	
- **Medium:** Largura igual ou superior a 600dp e inferior a 840dp. Representa a maioria dos tablets na orientação retrato e displays internos grandes dobrados.
	
- **Expanded:** Largura igual ou superior a 840dp e inferior a 1200dp. Representa tablets na orientação paisagem e telas internas de dobráveis abertos.
	
- **Large e Extra-large:** Existem também categorias para telas ainda maiores, como grandes tablets (1200dp a 1600dp) e desktops (acima de 1600dp).

A obtenção desse estado é feita calculando a métrica através da função `calculateWindowSizeClass`. 

![](../../../../attachments/Pasted%20image%2020260606081421.png)
![](../../../../attachments/Pasted%20image%2020260606081434.png)
 
- **Estratégia Recomendada (Progressiva):** A recomendação técnica estabelece que o projeto inicie focado no formato _Compact_. Em iterações posteriores, injeta-se o comportamento pertinente ao formato _Medium_ e, por fim, o suporte ao formato _Expanded_.

**Supporting Panel:** Usado para complementar o conteúdo principal com informações secundárias ou contexto.

**Feed Layout:** O Layout de Feed é usado para exibir um fluxo contínuo de conteúdo (ex: redes sociais, notícias).

**Cenas**: Uma Scene é capaz de renderizar uma ou mais instâncias de NavEntry. Pense em uma Scene como uma seção da sua interface de usuário que pode conter e gerenciar a exibição de conteúdo da back stack.