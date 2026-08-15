

---

O cliente relata os sintomas de um processo falho e, instintivamente, tenta formular uma resolução com base no seu próprio conhecimento, o qual geralmente é limitado. A **engenharia de requisitos** exige que o profissional não atue como um mero anotador de pedidos. É necessário aplicar técnicas de: coleta, extração e descoberta de informações para isolar a causa do problema.  Para encontrar a solução, a análise divide o projeto em duas áreas:
- **Domínio do Problema**
- **Domínio da Solução**

O analista deve esgotar e mapear o domínio do problema antes de permitir que a equipe de engenharia inicie o desenvolvimento do domínio de solução.

---

>[!tip] No máximo, você pode aumentar a probabilidade de alguém não encontrar um erro.

**Validação**: é validar se o que estamos construindo é que o cliente espera. É voltar ao doc de requisitos e ver se o que foi proposto é atendido.

**Verificação**: É verificar se o que foi construído funciona, se não tem bug, se é robusto.
- **Estática/Inspeções de software:** Inspeção é uma revisão cuidadosa, linha por linha, do código fonte. Pode ser inclusive no doc de requisitos. Objetivo é a DETECÇÃO de defeitos (não correção). Como linhas duplicadas, variáveis não usadas, code smells.
	[[2_Code smells|Entendendo CODE SMELLS]]
- **Dinamica/testes de software:** codigo executado. Verifica se o comportamento é o esperado.

---

**Pirâmide de testes**
![500](../../../attachments/Pasted%20image%2020260815142008.png)
- Teste unitarios e de compoenentes são responsabilidades do dev.
- Teste de integração e do sistema, são de responsabilidade do especialista em testes.


**Abordagens e teste**:

1. **Caixa branca/estrutural:** Nesta abordagem, o desenvolvedor possui acesso total ao código-fonte. O objetivo é testar a estrutura interna da aplicação, analisando os algoritmos implementados, os fluxos lógicos, as estruturas de repetição e de decisão.
	- **Ex:** A escrita de Testes Unitários.

2. **Caixa preta/funcional:**  Nesta metodologia, a estrutura interna do código-fonte é tratada como desconhecida. O teste é baseado no documento de requisitos. A validação foca exclusivamente na análise de entradas e saídas. 
	- **Ex**: O teste de uma API por meio de um cliente externo. O testador envia uma requisição e apenas verifica se o servidor retorna a mensagem de sucesso apropriada.
	
3. **Caixa cinza/híbrido**: O teste é conduzido e executado focado nas funcionalidades, como na Caixa Preta, mas o planejamento dos cenários de teste é auxiliado por um conhecimento parcial da arquitetura interna.
	- **Ex**: Ao testar um formulário de cadastro na interface do sistema, o testador preenche os dados e recebe a mensagem de sucesso na tela. Em seguida, ele acessa diretamente a infraestrutura do banco de dados para auditar se o registro foi armazenado na tabela correta e se a senha do usuário recebeu o algoritmo de criptografia adequado.

![400](../../../attachments/Pasted%20image%2020260814090559.png)
Os testes verificam a existência de defeitos
(**falhas**) em um software . ****
 Através da depuração é possível localizar e
remover **faltas**. Código incorreto ou ausente que, quando executado, pode
resultar em uma falha

**Tipos de manutenção: CAMP** 
1. **Corretiva:** correção de erros encontrados na verificação ou na validação.
2. **Adaptativa:** adaptação a mudansças externa.
3. **De melhoria/perfectiva:** melhorias requeridas pelos usuários.
4. **Preventiva/de reengenharia:** Abordagem pró-ativa com foco na melhoria da manutibilidade
