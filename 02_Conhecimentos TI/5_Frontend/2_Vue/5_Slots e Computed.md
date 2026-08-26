


---
### 1. Slots

Os Slots transmitem estruturas de interface ( HTML ou outros componentes). As vantagens são:
- Evita a criação de dezenas de propriedades apenas para tentar cobrir todas as variações visuais.
- Permite injetar marcação HTML nativa ou até mesmo outros componentes Vue inteiros para dentro do filho, o que é tecnicamente inviável e incorreto de se fazer utilizando Props.

O componente filho define sua estrutura CSS e de comportamento, mas deixa uma área aberta para que o texto ou ícone do botão seja definido externamente.![300](../../../attachments/Pasted%20image%2020260824114351.png)O pai instancia o componente filho e escreve o conteúdo HTML desejado entre as tags de abertura e fechamento do componente. O Vue compilará esse conteúdo e o transportará para o local exato do `<slot>`.![400](../../../attachments/Pasted%20image%2020260824114417.png)

---
### 2. Computed

Propriedades computadas O papel  das proprie é monitorar um ou mais estados reativos originais (como instâncias de `ref` ou `reactive`) e calcular automaticamente um novo valor sempre que as variáveis monitoradas sofrerem mutação na memória.

O valor resultante de uma propriedade computável é estritamente de leitura (_read-only_). O desenvolvedor não pode atribuir um dado manualmente a um `computed`; o dado existirá unicamente como o resultado da execução da função interna que o define.

### O Propósito Arquitetural

A existência da ferramenta `computed` soluciona dois problemas centrais na arquitetura de componentes do Vue: a separação de responsabilidades e o consumo excessivo de processamento.

- **Extração de Lógica do Template:** O bloco HTML (`<template>`) tem a responsabilidade exclusiva de renderizar a interface visual. Embutir regras matemáticas matemáticas de negócios, concatenação de cadeias de caracteres ou filtragem de matrizes diretamente nas tags HTML quebra a legibilidade do código. A propriedade computável extrai essa carga de processamento para o bloco de script, entregando ao HTML apenas o resultado final limpo.
    
- **O Mecanismo de Cache (Desempenho):** Esta é a diferença fundamental entre utilizar um `computed` e utilizar uma função padrão do JavaScript. O compilador do Vue armazena o resultado da propriedade computável na memória (cache). Se a tela for atualizada por qualquer outro evento, o Vue devolve o valor armazenado no cache imediatamente, sem executar a matemática novamente. O recálculo completo só será processado se, e somente se, as variáveis originais rastreadas dentro da função forem alteradas.
![500](../../../attachments/Pasted%20image%2020260826105921.png)