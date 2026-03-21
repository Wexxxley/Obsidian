


---

É recomendado criar arquivos Kotlin separados para cada tela.
![](../../attachments/Pasted%20image%2020260321090519.png)

**MainActivity**
![](../../attachments/Pasted%20image%2020260321094653.png)

**navController**: é o detentor de estado centralizado da navegação. Ele é o único objeto que realmente sabe "onde o usuário está".

- **Gerenciamento de Pilha:** Ele gerencia uma pilha, cada vez que você navega, ele empilha um nobo objeto de contexto. Ele que lida com a troca de
- **Sobrevivência a Reconfigurações:** Ao usar `rememberNavController()`, você está vinculando esse objeto ao ciclo de vida da Activity, garantindo que a pilha de telas não se perca se o usuário girar o celular (o que causaria a destruição da instância da Activity).
    

**NavHost** não é apenas um "container".
- Ele cria internamento um grafo de cenas
- Ele atua como um observador. Ele fica "escutando" as mudanças no NavController. 
- Ele é responsável por criar e destruir o `Lifecycle` de cada tela. 

---

## 3. startDestination: O Estado Inicial da Máquina

Em Teoria da Computação, toda máquina de estados precisa de um **Estado Inicial ($\mathbf{S_0}$)**. O `startDestination` é exatamente isso.

- **Ponto de Entrada Invariável:** Ele garante que o Grafo sempre tenha um nó raiz. Sem isso, o `NavHost` não saberia o que renderizar no primeiro frame do app.
    
- **Limpeza da Pilha:** O destino inicial é especial porque, por padrão, o sistema de navegação do Android tenta manter esse nó na base da pilha. Se o usuário apertar "voltar" na `startDestination`, o app fecha, pois não há mais estados para retroceder.
    

---

## 4. O Grafo de Navegação (NavGraph)

O bloco de código dentro das chaves do `NavHost` `{ ... }` é onde você define o **NavGraph**.

- **Registro de Destinos:** Cada função `composable("rota")` adiciona um vértice ao seu grafo.
    
- **Mapeamento de Rotas:** É um mapeamento do tipo `Map<String, ComposableFunction>`. Quando você navega para `"segunda_tela"`, o controlador faz uma busca (lookup) nessa tabela para encontrar o binário da função que deve ser executado.
    
