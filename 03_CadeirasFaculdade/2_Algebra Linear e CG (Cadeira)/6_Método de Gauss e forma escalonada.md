
#Concluded 

---
### **1. Forma escalonada e classificação de sistemas**
Uma matriz de ordem $m*n$ é está na forma escada quando: 
	[A] O primeiro elemento não nulo de uma linha não nula é 1.
	[B] Cada coluna que contém o primeiro lemento não nulo de uma linha tem todos os seus outros elementos ==abaixo iguais a zero==.
	[C] Toda linha nula ocorre abaixo de todas as linhas não nulas.
	[D] O número de zeros precedendo o primeiro elemento não nulo de uma linha aumenta a cada linha.  

>[!note]
Seja um sistema de equações lineares de $Q$ equaçoes e $K$ icógnitas. Seja $p_{a}$ o posto da matriz ampliada e $p_{c}$ o posto da matriz dos coeficientes. Então:
>1. Se $p_{a} = p_{c} = K$, possui uma única solução. ==Possível e determinado==
>2. Se $p_{a} = p_{c} \neq  K$, possui infinitas soluções. ==Possível e indeterminado==

O **grau de liberdade** do sistema é $K-p$. Onde $K$ é o número de icógnitas e p o posta da matriz ampliada do sistema.  O **grau de liberdade** em um sistema linear representa a quantidade de variáveis que podem ser escolhidas arbitrariamente para determinar as outras. Isso acontece porque temos mais incógnitas do que equações independentes.

---
### **2. Método de Gauss**
Dado um sistema de equações lineares, seguimos os seguintes passos para obter a solução:
1. Encontrar a matriz escalonada da matriz ampliada do sistema.
2. Calcular o posto da matriz ampliada e da matriz dos coeficientes.
3. Classificar o sistema
4. Calcular o grau de liberdade e calcular as soluções.

![](../../attachments/20260308_074127%20(1).jpg)
