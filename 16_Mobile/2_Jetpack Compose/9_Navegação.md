


---

É recomendado criar arquivos Kotlin separados para cada tela.
![](../../attachments/Pasted%20image%2020260321090519.png)

**MainActivity**
![](../../attachments/Pasted%20image%2020260321094653.png)

**navController**: é o detentor de estado centralizado da navegação. Ele é o único objeto que realmente sabe "onde o usuário está".
- **Gerenciamento de Pilha:** Ele gerencia uma pilha, cada vez que você navega, ele empilha um nobo objeto de contexto. Ele que lida com a troca de activitys
    
**NavHost** não é apenas um "container".
- Ele cria internamento um grafo de cenas
- Ele atua como um observador. Ele fica "escutando" as mudanças no NavController. 
- Ele é responsável por criar e destruir o `Lifecycle` de cada tela. 
- É preciso registrar as telas.
- É preciso ter um nó inicial. Por padrão, o sistema de navegação do Android tenta manter esse nó na base da pilha. Se o usuário apertar "voltar" o app fecha, pois não há mais estados para retroceder.

**NavGraph**: Nos/telas registradas.
- **Registro de Destinos:** Cada função `composable("rota")` registra um vértice.
- **Arestas** do grafo são operações de transição de estado. A aresta existe no momento da execução do comando `navController.navigate("rota")`.
- **Adjacência:** No seu `NavHost`, todos os destinos definidos dentro do mesmo bloco são, por padrão, adjacentes entre si. Isso significa que, teoricamente, qualquer tela pode navegar para qualquer outra, desde que possua a referência do `NavController`.
- **Propriedades da Aresta:** Você pode configurar propriedades na transição, como:
    - **Animações:** `enterTransition` e `exitTransition`.
    - **Comportamento da Pilha:** `launchSingleTop` (evita duplicar o vértice na pilha) ou `popUpTo` (remove vértices intermediários durante a transição).        


## 2. Níveis de Telas: O conceito de Subgrafos (Nested Navigation)

Se você quer um "nível a mais" de telas que não sejam acessíveis diretamente pelo nó principal (ou para organizar melhor a arquitetura), você utiliza o **Nested Navigation** (Navegação Aninhada).

- **O que é:** É a capacidade de criar um **Grafo dentro de outro Grafo**.
    
- **Encapsulamento:** Você agrupa destinos relacionados (ex: um fluxo de Login com 3 telas) dentro de um bloco `navigation`. Esse grupo passa a se comportar como um único "Super-Vértice" para o grafo principal.
