

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
![500](../../../attachments/Pasted%20image%2020260814082942.png)

O **TDD** (Test-Driven Development) e o **BDD** (Behavior-Driven Development) são práticas de desenvolvimento de software baseadas na escrita prévia de testes. O TDD foca na qualidade técnica do código e testes unitários, enquanto o BDD expande essa ideia para o comportamento do sistema e a colaboração com o negócio.


Teste unitario e de compoenentes sao responsabilidades do dev
Teste de integração do especialista em testes.

Após cada integração, o desenvolvedor precisa testar os elementos afetados para garantir que eu não incluiu defeitos que não existiam

- Testes de regressão




**Abordagens e teste**
**Caixa branca/estrutural:** Realizado a partir do conhecimento de detalhes da implementação. princiaplemnte usado pelo dev. teste unitario e de integração
**Caixa preta/funcional:** Os testes são planejados a partir de uma especificação abstrata. A implementação é desconhecida. princiaplemnte no Teste de sistema
**Caixa cinza/híbrido**: Testes de caixa preta com conhecimento limitado sobre a
implementação.

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
