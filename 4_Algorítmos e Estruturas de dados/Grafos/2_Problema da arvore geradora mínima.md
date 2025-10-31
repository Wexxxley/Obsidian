
#Concluded 

---
### 1. Árvore
Uma árvore é um **grafo conexo e acíclico**; Se é conexo, para qualquer par de vértices do grafo, existe pelo menos um caminho ligando esses dois vértices. Se é acíclico, o grafo não possui ciclos.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfWMRbyy5wl6gMQzlBRe4Pf-V2yG7RZm2M6OhNHSDLYXPtRSoArFEtENF1jrQGiOGT7ewIuBCGP7-IcGM39CugcEXywvXXcIUftsfdszB0DuADVtLnzbrNT_LhY-0dxjRFIaiktXg?key=VJjD-GQ4BeMLFSL3weHQfxOz)


1. Em uma árvore, a quantidade de arestas(E) é o número de vértices(V) - 1. <mark style="background: #ADCCFFA6;">|E|=|V| - 1.</mark>
    
2. Se removermos uma aresta da árvore, ela deixa de ser conexa. Ou seja, <mark style="background: #ADCCFFA6;">uma árvore é um grafo onde os vértices estão minimamente conectados.</mark>
    
3. Se T for árvore, ao adicionarmos uma nova aresta, criamos um ciclo em T. E podemos criar uma nova árvore ao removermos uma aresta do ciclo, diferente da aresta adicionada.

---
### 2. Subgrafo e subgrafo gerador

**Subgrafo**: Se $G′ = (V′ , E′ )$ for subgrafo de um grafo $G = (V, E)$, então $V′ ⊆ V e E′ ⊆ E$.

**Subgrafo gerador**: Um subgrafo $G′ = (V′ , E′ )$ é gerador quando $V′ = V$ e $E′ ⊆ E$. Eles são ditos geradores, por que a partir deles é possível retornar ao grafo original somente adicionando arestas.

Exemplos de subgrafos geradores. 
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcP097izxYt702KbZySGfpYR3sAjf9lVPr3muZFdtuB_bsktVnlUvBM65aBB8qxBk6FbplE5XQmJfg-SMsd7JCSSX3NxUQc7MJVJDb-8akqB1U3hObN49wDBX-Igid7TsVjEj62?key=VJjD-GQ4BeMLFSL3weHQfxOz)

---
### 3. Problema da subárvore geradora mínima

 Seja um grafo $G = (V, E)$ conexo e ponderado(possui peso). <mark style="background: #ADCCFFA6;">No problema da árvore geradora mínima, deseja-se encontrar a árvore geradora T de peso mais baixo</mark>. O peso de uma árvore geradora é o somatório de todos os pesos associados a uma aresta.

 
- **Análise de Dados (Clustering):** Usar o MST para visualizar "clusters". O software pode conectar todos os clientes (nós) com base na "dissimilaridade" (peso) entre eles. As arestas mais longas do MST, quando removidas, naturalmente separam os grupos de clientes.
    
- **Design de Microserviços:** Um software de arquitetura pode sugerir um "caminho de comunicação essencial" entre diferentes microserviços, minimizando o "custo" de dependência (peso) entre eles, garantindo que todos os serviços críticos possam trocar dados.
    

### 2. Software para o Setor Público (Estados)

- **Planejamento de Infraestrutura Rural:** Um software para o governo estadual planejar a expansão da rede de fibra óptica (ou saneamento), conectando todas as vilas (nós) com o menor custo total de cabeamento/tubulação (peso).
    
- **Redes de Sensores (Defesa Civil):** Um software que determina como conectar uma rede de sensores (ex: nível de rio, alerta de deslizamento) para que todos reportem a uma central, usando os links de comunicação (rádio, satélite) de menor custo ou menor consumo de energia (peso).
    
- **Logística de Vacinação:** Planejar a rede de distribuição de vacinas. Conectar todos os postos de saúde (nós) a um centro de distribuição central, otimizando as rotas de "abastecimento" (pesos) para garantir a cobertura total com o menor custo logístico de transporte.
    

### 3. Software para Coleta de Lixo (Logística)

> **Importante:** O MST _não_ calcula a rota diária do caminhão (isso é o "Problema do Caixeiro Viajante", que é diferente). O MST ajuda no **planejamento estratégico** da rede.

- **Setorização de Coleta:** Um software que ajuda a dividir a cidade em setores. O MST pode conectar todos os pontos de coleta (nós) pela distância (peso), e o software sugere "cortar" as arestas mais longas para criar zonas de coleta compactas e eficientes.
    
- **Planejamento de Estações de Transbordo:** Decidir onde construir pontos de transbordo (onde caminhões pequenos descarregam em carretas grandes). O MST conecta todos os bairros (nós) ao aterro sanitário (hub) com o menor custo total de transporte (peso), indicando os locais ideais para esses hubs intermediários.