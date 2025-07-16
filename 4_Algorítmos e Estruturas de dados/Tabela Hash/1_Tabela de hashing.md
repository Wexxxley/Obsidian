

---
 Muitas aplicações exigem um conjunto que suporte somente as operações de INSERT, SEARCH e DELETE.  Embora a busca por um elemento em uma tabela hash possa demorar O(n) no pior caso, na prática o hashing funciona extremamente bem. Sob premissas razoáveis, o tempo médio para pesquisar um elemento é O(1).

 Estrutura de dados do tipo **{key : data}** que fornecem apenas as operações de inserção, busca e remoção são chamados de **dicionários ou maps.**

| Ex: Queremos carregar um dicionário da língua portuguesa na memória do pc.                                                               |
| ---------------------------------------------------------------------------------------------------------------------------------------- |
| - Operações de inserção e busca serão frequentemente realizadas.<br>- Remoções podem ser realizadas e gostaríamos que fossem eficientes. |
### **1. Tabela de acesso direto**
O endereçamento direto é uma técnica simples que funciona bem quando o universo U de chaves é pequeno. O aspecto negativo é óbvio: se o universo é grande, muita memória será desperdiçada.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdEGpIS5a7rjIGJUS3pCFTu8grQPju-ODM4NxIOqkIukiH1GBdF3JcdyQ_SnfXTqbXPkMmK0fPJ-eZh2TWCbs6sPcWcqjtmCLe4l46WCPyIOWECZXFE-ff7cEUQjzBew-fMvBNY9w?key=VJjD-GQ4BeMLFSL3weHQfxOz)

### **2. Tabela hash**
Estrutura de dados onde as posições dos objetos armazenados são calculadas através de uma função hash que visa distribuir os elementos aleatoriamente ao longo de uma estrutura.
![600](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdjWfUvflkQZN7CXyMmlZh8oG2niDbBdt1geQqn6X40NAv3ooavE8Fm_A073j9JMMu0rflpsYnOf3VWO7Tq4PVA-MHgw-Pf9Urz2-TXlqpP-bUlhuP60dccQaNirM_Mq-KE11NKfA?key=VJjD-GQ4BeMLFSL3weHQfxOz)


### 2.1 Função de hashing

 Dado um conjunto de chaves K e um inteiro positivo M(total de slots), uma função de hashing h é uma função h: K → {0, 1, . . . , M − 1} que satisfaz as condições:

- Produz um número baixo de colisões. 
    
- É facilmente computável.
    

  

 Na prática, é conveniente implementar uma função de hashing h como a composição de duas funções f e g.

1. A função de codificação f mapeia chaves em inteiros não negativos:
    

f : K → Z≥0.

2. A função de compressão g mapeia o inteiro gerado em inteiros no conjunto {0, 1, . . . , M − 1}: g : Z≥0 → {0, . . . , M − 1} 
    

  

Função de codificação: Strings estão entre os tipos mais comuns de chaves. Suponha que temos um conjunto de chaves do tipo string e queremos construir uma função de codificação.  Então, dado um valor do tipo string, como transformá-lo em um inteiro positivo?

 Solução simples: Uma string é composta por uma cadeia de caracteres. Cada caractere é um inteiro cujo valor é determinado na tabela ASCII. A ideia é usar o valor ASCII de cada caractere da chave para compor o valor de retorno da função.

  

 Neste exemplo simples, cada caractere é multiplicado por 127 elevado a uma potência baseada na posição do caractere e depois tudo é somado. Dessa forma, é possível gerar um inteiro positivo com base em um string evitando colisões.

  

Função de compressão

 É preciso construir função g que mapeia qualquer inteiro x não negativo no conjunto {0, 1, . . . , M − 1}. A ideia é usar o módulo para obter o resto da divisão de x ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXecB9YAZpM7SdRWwofbikzjOh96EdYbm_Tb6i5BQLZKs7GZOQ2KUtyKGwKDUTi_MrQ2EYndLwb8C7g6bwiH1jmuRCz7rh1h6pxOE1qFXwO81kN-cu8aWVpyBDHegg7rImwtD71RCg?key=VJjD-GQ4BeMLFSL3weHQfxOz)

pelo tamanho M da tabela hash.  g(x) = x mod M

  

Escolhendo o tamanho do slot: Normalmente escolhemos M como um número primo. Escolha uma potência de 2 que esteja próxima do valor desejado de M. Depois, adote para M o número primo que esteja logo abaixo do número escolhido.

___________________________________________________________________________

### 1.3.2 Tratamento de colisão

#### 1.3.2.1 Encadeamento exterior

 Nessa técnica, em vez de armazenar um único valor em cada posição da tabela, cada posição armazena uma lista encadeada.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXebIWiz9PeHkkHpmvbWjedu2ZNgQwHNU34qldJ46mFVB6vAcC-EgTSUnVkozSHSUx1256o5X9o8EveWFjdxVPhX6zFn1_daJWMssPOt_Xyrve2tbW2ON93dDPXg5OdCfi9l2Ybmwg?key=VJjD-GQ4BeMLFSL3weHQfxOz)

#### 1.3.2.1 Sondagem linear

 Quando uma colisão ocorre, a sondagem linear busca uma posição vazia para armazenar o novo valor, verificando as posições subsequentes da tabela. Caso a posição alvo esteja ocupada, o algoritmo "avança" para a próxima posição, até encontrar um espaço livre.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdZXhACeae1QJAjL6U262J90iD0GvlYbKlUovE-4LBy-6V6oQi5C1MOzG5Zynczb4YXc2q62EHeW-zXw3z2ciqc2JrkEwyFkcMA9BaxNXHRnHAz4FvFAHEPT-ZRyzWJ3_LEHxE9?key=VJjD-GQ4BeMLFSL3weHQfxOz)

 A sondagem linear é o mais rápido se a tabela for esparsa. Já o encadeamento exterior é mais fácil de implementar, mas usa memória a mais para os ponteiros.

  

 Tabelas hash são ideais quando você precisa de desempenho rápido em operações de inserção, busca e remoção, mas sem a necessidade de manter os dados ordenados.

**