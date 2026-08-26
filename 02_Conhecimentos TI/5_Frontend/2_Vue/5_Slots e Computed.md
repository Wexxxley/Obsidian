
#Concluded 

---
### 1. Slots

Os Slots transmitem estruturas de interface ( HTML ou outros componentes). As vantagens são:
- Evita a criação de dezenas de propriedades apenas para tentar cobrir todas as variações visuais.
- Permite injetar marcação HTML nativa ou até mesmo outros componentes Vue inteiros para dentro do filho, o que é tecnicamente inviável e incorreto de se fazer utilizando Props.

O componente filho define sua estrutura CSS e de comportamento, mas deixa uma área aberta para que o texto ou ícone do botão seja definido externamente.![300](../../../attachments/Pasted%20image%2020260824114351.png)O pai instancia o componente filho e escreve o conteúdo HTML desejado entre as tags de abertura e fechamento do componente. O Vue compilará esse conteúdo e o transportará para o local exato do `<slot>`.![400](../../../attachments/Pasted%20image%2020260824114417.png)

---
### 2. Computed

O papel  das propriedades computadas é monitorar um ou mais estados reativos originais e calcular automaticamente um novo valor sempre que as variáveis monitoradas sofrerem mutação.

O valor resultante de uma propriedade computável é read-only. O desenvolvedor não pode atribuir um dado manualmente a um computed; o dado existirá como resultado da execução da função interna que o define.
![600](../../../attachments/Pasted%20image%2020260826105921.png)