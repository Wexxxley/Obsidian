
---
### **1. React**
**Objetivo Principal:** Construir interfaces de usuário interativas e reutilizáveis.
- **Arquitetura baseada em Componentes:** React quebra a interface em pedaços isolados e reutilizáveis chamados **componentes**. 
- **Estado Local:** Cada componente pode ter sua própria "memória" interna, chamada de estado. Por exemplo, um campo de busca precisa "lembrar" o que o usuário está digitando. Um menu dropdown precisa "lembrar" se está aberto ou fechado. 
- **Declarativo:** Você diz ao React **o que** quer que apareça na tela com base no estado atual, e o React se encarrega de descobrir **como** atualizar a tela da forma mais eficiente possível. 
- **JSX**: O react usa o JSX (JavaScript XML). É uma união entre JavaScript e HTML.

> O navegador não entende JSX diretamente. Antes de o código ser executado, uma ferramenta de `build` (como o Vite) traduz o código JSX para JavaScript puro que o navegador entende.

#### **Diferenças entre JSX e HTML Puro**

1. **Atributo `class` vira `className`**
    ```jsx
    <div className="card product">...</div>
    ```
2. **Expressões JavaScript**: Você pode injetar qualquer expressão JavaScript (variáveis, funções, operações) diretamente no seu "HTML" envolvendo-a em chaves `{}`.     
    ```jsx
    const nome = "Maria";
    const elemento = <h1>Olá, {nome}!</h1>; // Dinâmico e direto
    
    const preco = 50;
    const elemento2 = <p>Preço: R$ {preco * 2}</p>; // Pode ter lógica
    
    const urlImagem = "https://i.imgur.com/logo.png";
    const elemento3 = <img src={urlImagem} />; // Usado em atributos
    ```
3. **Estilos em Linha são Objetos**:  Em JSX, ele recebe um objeto js. As propriedades CSS que têm hífens (como `font-size`) são escritas em `camelCase` (como `fontSize`).
    ```jsx
    //chaves duplas: a primeira para injetar JS, a segunda para o objeto.
    <div style={{ backgroundColor: 'blue', fontSize: '16px' }}></div>
    ```
#### 5. Um Único Elemento Raiz por Componente

Um componente React só pode retornar **um único elemento "pai"**. Se você precisar retornar múltiplos elementos adjacentes, você deve envolvê-los em um elemento pai.

- **Isto causa um ERRO:**
    
    JavaScript
    
    ```
    return (
      <h1>Título</h1>
      <p>Parágrafo</p> // Erro! Dois elementos no nível superior.
    );
    ```
    
- **Solução: Usar `Fragments`** Para não adicionar `divs` desnecessárias ao seu HTML, use um **Fragment**, que é representado por `<> ... </>`.
    
    JavaScript
    
    ```
    return (
      <>
        <h1>Título</h1>
        <p>Parágrafo</p>
      </> // Correto! O Fragment serve como um elemento pai invisível.
    );
    ```
    

#### 6. Atributo `for` vira `htmlFor`

Assim como `class`, a palavra `for` é reservada em JavaScript (para laços de repetição `for (...)`). Portanto, em `labels`, você deve usar `htmlFor`.

- **HTML Puro:**
    
    HTML
    
    ```
    <label for="username">Usuário:</label>
    <input id="username" type="text" />
    ```
    
- **JSX:**
    
    JavaScript
    
    ```
    <label htmlFor="username">Usuário:</label>
    <input id="username" type="text" />
    ```

### **2. Vite**

**Objetivo Principal:** Servir como uma ferramenta de `build` e um servidor de desenvolvimento **extremamente rápido** para projetos web modernos. Vite não faz parte da sua aplicação final, mas é a ferramenta que você, desenvolvedor, usa todos os dias. Ele resolve dois grandes problemas:

1. **Velocidade de Desenvolvimento:**
    - **Servidor de Desenvolvimento Instantâneo:** O Vite usa módulos nativos do navegador, ele inicia o servidor de desenvolvimento quase que instantaneamente.
    - **Hot Module Replacement Rápido:** Quando você salva uma alteração em um arquivo, o Vite atualiza apenas aquele "módulo" específico no navegador, sem recarregar a página inteira. O resultado é uma atualização quase imediata na tela.
2. **Otimização para Produção:**
    - Quando você termina o projeto e precisa gerar os arquivos finais para hospedar na internet, o Vite otimiza tudo: ele minifica o código (remove espaços e encurta nomes), divide o código em pedaços menores (code splitting) para um carregamento mais rápido, e muito mais.

### **3. Redux**
**Objetivo Principal:** Gerenciar o **estado global** da sua aplicação de forma previsível, centralizada e depurável.

O `useState` do React é ótimo para o estado local de um componente. Mas e se vários componentes, em partes completamente diferentes da sua aplicação, precisarem acessar ou modificar a **mesma informação**?

**Exemplos de Estado Global:**
- Informações do usuário logado (token, nome, permissões).
- O conteúdo de um carrinho de compras.
- O tema do site (claro ou escuro).

É aqui que o Redux entra.
- **Store Centralizada:** Redux cria uma "Store" (loja), que é um único objeto JavaScript que vive fora de todos os componentes. Essa Store é a **única fonte da verdade** para o estado global da sua aplicação.