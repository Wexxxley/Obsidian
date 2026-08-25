

---
### 1. Props
Props são atributos personalizados registrados na estrutura de um componente filho. Elas representam o mecanismo oficial para a transferência unidirecional de dados do componente pai para o componente filho.
![500](../../../attachments/Pasted%20image%2020260824111352.png)![](../../../attachments/Pasted%20image%2020260824111336.png)
**1. Passagem de dado Estático:** você declara `titulo="Servidor Central"`.
**2. Passagem Dinâmica:** é preciso usar v-bind.

---
### 2. Slots

Os Slots transmitem estruturas de interface ( HTML ou outros componentes). As vantagens são:
- Evita a criação de dezenas de propriedades apenas para tentar cobrir todas as variações visuais.
- Permite injetar marcação HTML nativa ou até mesmo outros componentes Vue inteiros para dentro do filho, o que é tecnicamente inviável e incorreto de se fazer utilizando Props.

O componente filho define sua estrutura CSS e de comportamento, mas deixa uma área aberta para que o texto ou ícone do botão seja definido externamente.![300](../../../attachments/Pasted%20image%2020260824114351.png)O pai instancia o componente filho e escreve o conteúdo HTML desejado entre as tags de abertura e fechamento do componente. O Vue compilará esse conteúdo e o transportará para o local exato do `<slot>`.![400](../../../attachments/Pasted%20image%2020260824114417.png)