

---
Até agora, utilizamos dados síncronos. Em aplicações reais, os dados vêm de uma API remota e chegam de forma assíncrona. Antes de conectarmos a uma API real, simularemos esse comportamento para entender o ciclo de renderização assíncrono.

O objetivo técnico é transformar a lista `stories` de um estado inicial síncrono para um estado que começa vazio e é preenchido após a resolução de uma _Promise_.

![](../../attachments/Pasted%20image%2020251125133327.png)

**1. Simulação da API (`getAsyncStories`)** Criamos uma função fora do componente que retorna uma **Promise**.

- A Promise é usada em JavaScript para operações que vão terminar no futuro.
    
- Utilizamos o `setTimeout` para forçar um atraso de 2000ms (2 segundos), simulando a latência de rede de uma requisição real.
    
- Quando o tempo acaba, a Promise "resolve" e entrega o objeto de dados (`{ data: { stories: ... } }`) .
    

**2. Inicialização do Estado (`useState([])`)** Mudamos a inicialização de `const [stories, setStories]`.

- **Antes:** `useState(initialStories)` - Os dados já estavam lá na primeira renderização.
    
- **Agora:** `useState([])` - A aplicação inicia com uma lista vazia. Isso reflete a realidade: quando o componente monta, a "requisição" ainda não foi feita ou não retornou .
    

**3. O Efeito de Busca (`useEffect`)** Introduzimos o hook `useEffect` para disparar a busca dos dados.

- Chamamos `getAsyncStories()` dentro do efeito.
    
- Usamos `.then()` para esperar a Promise resolver. Quando os dados chegam (após 2 segundos), chamamos `setStories` para atualizar o estado.
    
- **Array de dependências vazio `[]`:** Isso é crucial. Garante que essa busca aconteça apenas **uma vez**, quando o componente é montado (aparece na tela pela primeira vez) .
    

**Resultado Visual:** Ao rodar este código, você verá a tela com o título e o input, mas a lista estará vazia. Após 2 segundos, a lista de histórias aparecerá.