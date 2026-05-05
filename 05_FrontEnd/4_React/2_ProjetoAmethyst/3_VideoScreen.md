


---
### **1. Estados**

![](../../../attachments/Pasted%20image%2020251127084154.png)
- **analysis**: É o container de resposta. Ele armazena o objeto JSON final que oGemini devolve.    
    - Se for uma palavra: `{ type: 'word', data: { definition: "...", grammar_class: "Noun", examples: [...] } }`
    - Se for uma frase: `{ type: 'sentence', data: { explanation: "...", nuances: "..." } }`

- **loadingAnalysis**: É o sinalizador de espera. Quando vira true, a caixa da esquerda mostra o spinner girando.
	- **disabled={loadingAnalysis}:** Isso impede que o usuário clique freneticamente em várias palavras enquanto a IA ainda está pensando na primeira.

- **selectedText**:  É a memória do clique. Guarda a string exata que o usuário quer investigar.

- **outputLang**: Define em qual língua a explicação deve ser gerada.

- **player**: Diferente de um vídeo HTML normal, o YouTube roda dentro de um iframe. A biblioteca `react-youtube` nos devolve um **objeto** que tem métodos especiais. Precisamos guardar esse objeto no estado para usá-lo depois.
    
- **activeIndex**: Se for 5, significa que a 6ª frase da lista deve estar em destaque. Se for -1, ninguém está falando nada.
    
- **useRef([])**: O useRef cria uma variável que **não dispara re-renderização** quando muda. Usamos ele para guardar referências às divs de cada legenda, para podermos mandar o navegador "rolar a tela" até elas.

---
### **2. Efeitos**

![](../../../attachments/Pasted%20image%2020251128080137.png)
- **setInterval**: Função nativa do Javascript. Diz "Execute o que está aqui dentro repetidamente, a cada X milissegundos." O timer é guardado dentro de interval.
- **clearInterval**: Pega a variável 'interval' e MATA o timer. Se não fizermos isso, o navegador continua rodando o código pra sempre.
- .**findIndex**:  percorre o array de legendas item por item. Para cada, ele testa a fórmula.
	- **currentTime >= sub.start**: O tempo atual é maior ou igual ao tempo de início da frase?
	- **currentTime < (sub.start + sub.duration)**: O tempo atual é menor que o tempo final da legenda.
- **Dependencies Array**: Se o 'player', as 'legendas' ou o 'índice ativo' mudarem, reinicie essa função useEffect.

![](../../../attachments/Pasted%20image%2020251128081456.png)
- Quando o activeIndex muda é preciso que a lista role sozinha para acompanhar.
- Aqui usamos o subtitleRefs. Se a legenda ativa é a 10, ele pega subtitleRefs.current[10] e chama a função nativa do navegador scrollIntoView.

