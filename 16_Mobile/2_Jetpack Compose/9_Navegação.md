


---
É recomendado criar arquivos Kotlin separados para cada tela.
![](../../attachments/Pasted%20image%2020260321090519.png)
![200](../../attachments/telas.gif)

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
    - **launchSingleTop**: Este parâmetro evita duplicatas  de tela na árvore em caso de erro de logica ou duplo clique no topo da pilha
    - **popUpTo**: Remove vértices intermediários durante a transição. Pense em um fluxo de Login: `Login` -> `Cadastro`. Quando o usuário finaliza o cadastro e vai para a `Home`, você não quer que ele consiga voltar para a tela de `Cadastro` ou `Login`.

**MainPage**
![550](../../attachments/Pasted%20image%2020260321101244.png)
![550](../../attachments/Pasted%20image%2020260321101545.png)
**Injeção de dependência:** A MainPage não cria o controlador; ela o recebe da MainActivity. Isso permite que a tela dispare eventos de navegação sem precisar saber como o Grafo de Navegação foi construído. Ela apenas dá a ordem, e o `NavController` (que tem a visão global da pilha) a executa.
**navigate**: Está sendo usando uma Template String para montar uma URL dinâmica.

**SecondPage**
![](../../attachments/Pasted%20image%2020260321102409.png)
Diferente da versão anterior onde os dados eram fixos ("David", "25"), agora a função recebe `name: String` e `age: String`.

- **O Conceito:** No Jetpack Compose, as telas devem ser, idealmente, **Stateless** (sem estado interno próprio sobre os dados que exibem).
    
- **A Importância:** Ao receber os dados via parâmetros, a `SecondPage` torna-se um componente de exibição puro. Ela não precisa saber de onde os dados vieram (se foi da `MainPage`, de um banco de dados ou de uma API); ela apenas renderiza o que o `NavHost` injetou nela durante a extração do `backStackEntry`.
    

## 2. O Método `popBackStack()` (Desempilhamento)

No `IconButton` da `TopAppBar`, temos a instrução: `navController.popBackStack()`.

- **Operação de Pilha:** Como estudante de CC, você reconhece isso como a operação **Pop** em uma estrutura de dados de Pilha (**Stack**).
    
- **O que acontece na memória:** 1. O `NavController` identifica a `NavBackStackEntry` atual (a da `SecondPage`). 2. Ele remove esse objeto do topo da pilha. 3. O ciclo de vida dessa tela é encerrado e ela é removida da memória (Garbage Collected). 4. O foco volta para o nó imediatamente abaixo na pilha (a `MainPage`).
    
- **Estado Preservado:** Como a `MainPage` não foi destruída (ela estava apenas em "stop" na pilha), ao voltar, os campos de texto (`username` e `userAge`) ainda conterão os valores que você digitou anteriormente.
    

## 3. Navigation Icon e Acessibilidade

O uso do parâmetro `navigationIcon` dentro da `TopAppBar` é o padrão de design para navegação hierárquica.

- **`Icons.AutoMirrored.Filled.ArrowBack`**: Esta é uma escolha técnica importante para internacionalização. O "AutoMirrored" garante que, em sistemas de escrita da direita para a esquerda (como o árabe), a seta aponte automaticamente para o lado correto sem que você precise mudar o código.
