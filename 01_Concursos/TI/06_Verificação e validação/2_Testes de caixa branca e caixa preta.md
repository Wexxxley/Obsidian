

---
### **1. Teses de caixa branca/de vidro**

Também conhecido como: teste baseado em código, teste estrutural.

São teste que levam em consideração o funcionamento interno de um sistema ou componente. Testes planejados com conhecimento da estrutura e da implementação do software.

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

**Complexidade ciclomática:** métrica que fornece uma medida quantitativa da complexidade do programa. Ajuda a identificar a quantidade de caminhos independentes que existem no sistema que fornecem o número de casos de testes necessários para garantir que
todos os comandos tenham sido executados pelo menos 1 vez.
- Um caminho único é qualquer caminho que adiciona ao menos 1 novo comando ou condição 

Para simplificar, usaremos complexidade ciclomática como:
- Número de decisões lógicas + 1
- Para condições compostas (a and b or c) somar um para cada condição.