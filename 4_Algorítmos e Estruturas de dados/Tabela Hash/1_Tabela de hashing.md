
#Concluded 

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

