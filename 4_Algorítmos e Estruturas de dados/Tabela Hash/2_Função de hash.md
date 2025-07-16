
#Concluded 

---
### **1. Função de hash**
Dado um conjunto de chaves K e M(total de slots), uma função de hashing h é uma função 
**h: K → {0, 1, . . . , M − 1}** que satisfaz as condições:
- Produz um número baixo de colisões. 
- É facilmente computável.

É conveniente implementar uma função de hashing h como a composição de duas funções f e g.
- **A função de codificação f** mapeia chaves em inteiros não negativos:
	- ==f : K → Z≥0.==
- **A função de compressão g** mapeia o inteiro gerado em inteiros no conjunto {0, 1, . . . , M − 1}:
	- ==g : Z≥0 → {0, . . . , M − 1}== 
    
#### **1.1 Função de codificação**
Strings estão entre os tipos mais comuns de chaves. Suponha que temos um conjunto de chaves do tipo string e queremos construir uma função de codificação.  Então, dado um valor do tipo string, como transformá-lo em um inteiro positivo?

**Solução simples:** Uma string é composta por uma cadeia de caracteres. Cada caractere é um inteiro cujo valor é determinado na tabela ASCII. A ideia é usar o valor ASCII de cada caractere da chave para compor o valor de retorno da função.

Neste exemplo, cada caractere é multiplicado por 127 elevado a uma potência baseada na posição do caractere e depois tudo é somado. Dessa forma, é possível gerar um inteiro positivo com base em um string evitando colisões.
#### **1.2 Função de compressão**
É preciso construir função a g que mapeia um inteiro x não negativo no conjunto {0, . . . , M−1}. A ideia é usar o módulo para obter o resto da divisão de x 
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXecB9YAZpM7SdRWwofbikzjOh96EdYbm_Tb6i5BQLZKs7GZOQ2KUtyKGwKDUTi_MrQ2EYndLwb8C7g6bwiH1jmuRCz7rh1h6pxOE1qFXwO81kN-cu8aWVpyBDHegg7rImwtD71RCg?key=VJjD-GQ4BeMLFSL3weHQfxOz)

Pelo tamanho M da tabela hash.  g(x) = x mod M

**Escolhendo o tamanho do slot:** Normalmente escolhemos M como um número primo. Escolha uma potência de 2 que esteja próxima do valor desejado de M. Depois, adote para M o número primo que esteja logo abaixo do número escolhido.

---
### **2. Tratamento de colisão**

#### **2.1 Encadeamento exterior**
Nessa técnica, em vez de armazenar um único valor em cada posição da tabela, cada posição armazena uma lista encadeada.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXebIWiz9PeHkkHpmvbWjedu2ZNgQwHNU34qldJ46mFVB6vAcC-EgTSUnVkozSHSUx1256o5X9o8EveWFjdxVPhX6zFn1_daJWMssPOt_Xyrve2tbW2ON93dDPXg5OdCfi9l2Ybmwg?key=VJjD-GQ4BeMLFSL3weHQfxOz)

#### **2.2 Sondagem linear**
Quando uma colisão ocorre, a sondagem linear busca uma posição vazia para armazenar o novo valor, verificando as posições subsequentes da tabela. Caso a posição alvo esteja ocupada, o algoritmo "avança" para a próxima posição, até encontrar um espaço livre.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdZXhACeae1QJAjL6U262J90iD0GvlYbKlUovE-4LBy-6V6oQi5C1MOzG5Zynczb4YXc2q62EHeW-zXw3z2ciqc2JrkEwyFkcMA9BaxNXHRnHAz4FvFAHEPT-ZRyzWJ3_LEHxE9?key=VJjD-GQ4BeMLFSL3weHQfxOz)

A sondagem linear é o mais rápido se a tabela for esparsa. Já o encadeamento exterior é mais fácil de implementar, mas usa memória a mais para os ponteiros.


### 3. 