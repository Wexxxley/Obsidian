


---

- Testes devem planejados muito antes de serem executados.
- **Princ de Pareto:** "80% dos erros acontecem em 20% dos componentes". Foque no essencial.
- Testes devem começar pequenos e progredir para pedaços maiores.
- Preferencialmente devem ser conduzidos por terceiros (exceto testes unitários), mas na prática não é assim.
- Um bom teste deve ter alta probabilidade de encontrar erros e não deve ser redundante.
### **1. Teses de caixa branca/de vidro**

Também conhecido como: teste baseado em código, teste estrutural. São teste que levam em consideração o funcionamento interno de um sistema ou componente. Testes planejados com conhecimento da estrutura e da implementação do software.

O objetivo é fornecer uma boa **cobertura de testes** (testes unitários e de integração)
- **Cobertura de comandos:** só precisa que todo comando seja executado.
- **Cobertura de funções:** só precisa que toda função/método seja executado.
- **Cobertura de caminhos:** conta quantos caminhos distintos foram testados.

Quando a quantidade de testes para um metodo cresce demais (mais do que as regras de negócio pedem) pode indicar que necessita de refatoração.

**Passos:** 
1. Gerar o grafo do código a ser avaliado.
2. Calcular a complexidade ciclomática.
3. Identificar os casos de teste baseado em:
	- Comandos
	- Caminhos
4. Calcular a cobertura.

![450](../../../attachments/Pasted%20image%2020260827131047.png)

**Complexidade ciclomática:** métrica que fornece uma medida quantitativa da complexidade do programa. Ajuda a identificar a quantidade de caminhos independentes que existem.
- Um caminho único é qualquer caminho que adiciona ao menos 1 novo comando ou condição 

Para simplificar, usaremos complexidade ciclomática como:
- Número de decisões lógicas + 1
- Para condições compostas (a and b or c) somar um para cada condição.

---
### 2. Testes de caixa preta/fechada

Teste funcional ou teste opaco. Testes que não levam em consideração o funcionamento interno dos componentes. Mesmo que tenha acesso ao código, este não é usado. São utilizados as especificações/requisitos para criar os testes.

Verificar se o software desenvolvido atende aos requisitos especificados. Os casos de teste podem ser planejados assim que as especificações são feitas
- Entradas válidas são aceitas e geram as saídas esperadas e entradas inválidas geram as mensagens de erro esperadas
- Encontrar coisas que não foram implementadas
- Requisitos não claros ou mal escritos afetam a qualidade dos casos de teste.

**Passo a passo:**
1. A especificação de requisitos é analisada.
2. Entradas válidas e inválidas são escolhidas.
3. As saídas esperadas para as entradas escolhidas são determinadas.
4. Os casos de testes são construídos.
5. O conjunto de teste é executado.
6. As saídas obtidas são comparadas com as saídas esperadas.
7. Um relatório é gerado para avaliar o resultado dos testes.

![500](../../../attachments/Pasted%20image%2020260828132109.png)
**Particionamento de equivalência**: O domínio de entrada é dividido em classes e os testes são gerado de modo a atingi-las de forma não redundante.
![](../../../attachments/Pasted%20image%2020260828132209.png)

**Valor limite**: Sabe-se que a maioria dos erros acontece nos limites das classes, tomando como base as classes de equivalência. 
- Testar limite -1;
- Testar limite;
- Testar limite +1.


---
![](../../../attachments/Pasted%20image%2020260828175802.png)CORRETO
![](../../../attachments/Pasted%20image%2020260828175844.png)Falso. Os de caixa preta os testadores que realizam.
![](../../../attachments/Pasted%20image%2020260828175854.png)
Falso. os de caixa preta nao dependem de código fonte

![](../../../attachments/Pasted%20image%2020260828180131.png)
CORRETO.
![](../../../attachments/Pasted%20image%2020260828180140.png)
ERRADO. As maneiros estretégicas de aplicar testes de software estão relacionadas a: testes unitario, teste de integração e teste de sistema

![](../../../attachments/Pasted%20image%2020260828181310.png)
FALSA. Seria correto de fosse no teste caixa branca.

![](../../../attachments/Pasted%20image%2020260828181359.png)Falso. Quanto mais integrado, mais testes de caixa preto são usados.

