
---
[[1_Introdução a grafos|1_Introdução a grafos]]

Redes são abstraidas através de um grafo não direcionado com pesos.

![[Pasted image 20250531092212.png]]
---

#### **1.1 Algortimos de roteamento**

**Algoritmo de roteamento global:** 
- calcula o caminho de menor custo entre uma origem e um destino usando conhecimento completo e global sobre a rede. 
- E isso exige que o algoritmo obtenha essas informações, de algum modo, antes de realizar de fato o cálculo. 
- Este pode ser rodado em um local (um algoritmo de roteamento global centralizado) ou replicado em vários locais. 

**Algoritmo de roteamento descentralizado:** o cálculo do caminho de menor custo é realizado de modo iterativo e distribuído. Nenhum nó tem informação completa sobre os custos de todos os enlaces da rede. 
- Em vez disso, cada nó começa sabendo apenas os custos dos enlaces diretamente ligados a ele. Então, por meio de um processo iterativo de cálculo e de troca de informações com seus nós vizinhos (isto é, que estão na outra extremidade dos enlaces aos quais ele próprio está ligado), um nó gradualmente calcula o caminho de menor custo até um destino ou um conjunto de destinos. O algoritmo de roteamento descentralizado que estudaremos logo adiante na Seção 4.5.2 é denominado algoritmo de vetor de distâncias (distance-vector algorithm — DV), porque cada nó mantém um vetor de estimativas de custos (distâncias) de um nó até todos os outros nós da rede.