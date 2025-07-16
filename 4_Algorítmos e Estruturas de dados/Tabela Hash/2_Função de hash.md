
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

![600](https://lh7-rt.googleusercontent.com/docsz/AD_4nXebIWiz9PeHkkHpmvbWjedu2ZNgQwHNU34qldJ46mFVB6vAcC-EgTSUnVkozSHSUx1256o5X9o8EveWFjdxVPhX6zFn1_daJWMssPOt_Xyrve2tbW2ON93dDPXg5OdCfi9l2Ybmwg?key=VJjD-GQ4BeMLFSL3weHQfxOz)

#### **2.2 Sondagem linear**
Quando uma colisão ocorre, a sondagem linear busca uma posição vazia para armazenar o novo valor, verificando as posições subsequentes da tabela. Caso a posição alvo esteja ocupada, o algoritmo "avança" para a próxima posição, até encontrar um espaço livre.

![600](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdZXhACeae1QJAjL6U262J90iD0GvlYbKlUovE-4LBy-6V6oQi5C1MOzG5Zynczb4YXc2q62EHeW-zXw3z2ciqc2JrkEwyFkcMA9BaxNXHRnHAz4FvFAHEPT-ZRyzWJ3_LEHxE9?key=VJjD-GQ4BeMLFSL3weHQfxOz)

A sondagem linear é o mais rápido se a tabela for esparsa. Já o encadeamento exterior é mais fácil de implementar, mas usa memória a mais para os ponteiros.

---
### **3. Quando usar e nao usar tabela hash**
Tabelas hash são ideais quando você precisa de desempenho rápido em operações de inserção, busca e remoção, mas sem a necessidade de manter os dados ordenados.
#### **1. Mapeamentos**
Qualquer situação onde você precisa "mapear" uma informação para outra.
- **Cenário:** Você tem a sigla de um estado e precisa do nome completo. Ou você tem um código de produto e precisa do seu preço.
    - **Chave:** `"CE"`.
    - **Valor:** `"Ceará"`.
#### **3. Contagem de Frequência de Itens**
Quando você precisa contar quantas vezes cada item aparece em uma coleção de dados.
- **Cenário:** Contar a frequência de cada palavra em um livro ou contar o número de votos para cada candidato em uma eleição.
- **Como funciona:** Você percorre a lista de itens. Para cada item:
    1. Verifica se ele já existe como chave na tabela hash.
    2. Se sim, incrementa o valor (o contador).
    3. Se não, adiciona o item como uma nova chave com o valor 1.
#### **3. Verificação de Itens Únicos (Implementando um "Set")**
Quando você precisa garantir que não há duplicatas em uma coleção. A estrutura de dados `Set` é, por baixo dos panos, uma tabela hash.
- **Cenário:** Você recebe uma lista com 1 milhão de e-mails e precisa gerar uma nova lista contendo apenas os e-mails únicos.
	- Você cria uma tabela hash/set. Para cada e-mail da lista original, você tenta adicioná-lo ao `Set`. A própria estrutura da tabela hash garante que duplicatas serão ignoradas.
#### **4. Quando NÃO usar uma Tabela Hash?**
1. **Quando a ordem dos elementos é importante**
2. **Quando você precisa de buscas por proximidade** 
3. **Quando o consumo de memória é extremamente crítico:** Tabelas hash podem usar mais memória do que um simples array, pois precisam de espaço extra para evitar colisões.