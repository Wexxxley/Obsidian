
#Concluded 

---
### **1. Grafos**

 Um grafo ==$G = (V, E)$== consiste em um ==conjunto de vértices (V)== e um ==conjunto de arestas (E)==. Cada aresta é um par $(v,w)$,  onde $v,w ∈ V$.

 - Se o par tiver direção, o grafo é **direcionado**. 
 - O vértice w é adjacente a v se, e somente se, (v,w) ∈ E. 
 - Um **caminho** em um grafo é uma sequência de vértices w1,w2,w3,…,wN tal que (wi,wi+1) ∈ E, ou seja, são adjacestes. 
 - Um grafo **não direcionado** é **conexo** se houver um caminho de qualquer vértice para qualquer outro vértice. Um grafo **direcionado** com essa propriedade é chamado de fortemente conexo.
 - Se um grafo **direcionado** não é fortemente conexo, mas seu **grafo subjacente** (o mesmo grafo sem considerar a direção das arestas) é conexo, então ele é chamado de **fracamente conexo**.
 - Um **grafo completo** é um grafo em que existe uma aresta entre cada par de vértices.

___
### **2. Representação de grafos**

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfH6clvRtr8C23J8Ff5Hq-LOek1BcgvQ7StRsr3FmFQiLs1i_-vgQJWCJBnUY7vs-7SJSnKZZ4f9EsjekLAO7UgKKkUe5X08iaNu5_H1E89xEHhlyJuxiU_-_cbzcRHNm-suELs?key=VJjD-GQ4BeMLFSL3weHQfxOz)

#### **2.1 Matriz de Adjacência**
Para um grafo com N vértices, a matriz de adjacência é uma matriz quadrada N×N.

- Para cada aresta (u,v), a entrada `A[u][v]` é definida como `verdadeiro`(`1`).
- Caso contrário, a entrada será `falsa`(`0`).
- Se a aresta tiver um **peso** associado, `A[u][v]` pode armazenar esse peso. Nesse caso: Um valor muito grande (∞) pode indicar a inexistência de uma aresta.

**Desvantagens da Matriz de Adjacência:**
- Embora seja **simples** de entender e implementar, é **muito ineficiente** em termos de espaço.
- Isso ocorre porque, em **grafos esparsos** (aqueles com relativamente poucas arestas em comparação com o número máximo possível de arestas), a maioria dos valores na matriz será nula, resultando em **desperdício de memória**.

#### **2.2 Listas de Adjacência**
Uma solução melhor para **grafos não densos (esparsos)** é o uso de listas de adjacência.

- Para cada vértice v, mantemos uma **lista de todos os vértices adjacentes** a ele.
- As listas de adjacência são o **padrão** para representar grafos na maioria das aplicações.
- Em **grafos não direcionados**, cada aresta (u,v) aparecerá em duas listas: v estará na lista de adjacência de u, e u estará na lista de adjacência de v.


  
  
  
**