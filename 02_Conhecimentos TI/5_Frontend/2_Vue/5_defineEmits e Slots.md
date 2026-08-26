
---
### 1. defineEmits 

Permite que o componente filho informe ao componente pai que uma interação física específica foi realizada pelo usuário na interface.
- O componente filho intercepta um evento do navegador e dispara um sinal nomeado. O componente pai monitora o surgimento desse sinal e, ao interceptá-lo, invoca uma função própria que contém os algoritmos lógicos e as regras de negócio do sistema.
- **Quando usar:** estritamente para acionar lógicas de processamento.

>[!TIP]
>- Se o componente filho so precisa mostrar os dados do pai: **defineProps**.
>- Se o componente filho precisa fornecer um dado para o pai: **defineModel**.
>- Se o componente filho precisa ordenar uma execução para o pai: **defineEmits**.


----
### 2. Slots

Os Slots transmitem estruturas de interface ( HTML ou outros componentes). As vantagens são:
- Evita a criação de dezenas de propriedades apenas para tentar cobrir todas as variações visuais.
- Permite injetar marcação HTML nativa ou até mesmo outros componentes Vue inteiros para dentro do filho, o que é tecnicamente inviável e incorreto de se fazer utilizando Props.

O componente filho define sua estrutura CSS e de comportamento, mas deixa uma área aberta para que o texto ou ícone do botão seja definido externamente.![300](../../../attachments/Pasted%20image%2020260824114351.png)O pai instancia o componente filho e escreve o conteúdo HTML desejado entre as tags de abertura e fechamento do componente. O Vue compilará esse conteúdo e o transportará para o local exato do `<slot>`.![400](../../../attachments/Pasted%20image%2020260824114417.png)