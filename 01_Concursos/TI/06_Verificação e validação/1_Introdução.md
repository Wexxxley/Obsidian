


Quem trabalha com requsisitos tem que entender, com base no pedido do cliente, o problema real, n necesariamente realizar a solução que o cliente sugeriu. É identifcar a melhor solução pro problema real.

No máximo vc pode aumentar a probabilidade de alguém n encontrar um erro.

**Validação**: é voltar ao doc de requisitos /cliente e ver se o que foi feito é o que ele queria, o que foi proposto, se ele valida.

**Verificação**: n é se eu entedi direito, é se o que construi n quebra, se n tem bug, se é robusto.
- **Estática/Inspeções de software:** n executa codigo. pode ser inclusive no doc de requisitos. linhas duplicadas, var n usados, metodos que fz mais de uma coisa. codes semels. 
- **Dinamica/testes de software:** codigo executado. Verifica se o comportamento é o esperado.

![500](../../../attachments/Pasted%20image%2020260814082942.png)

O **TDD** (_Test-Driven Development_) e o **BDD** (_Behavior-Driven Development_) são práticas de desenvolvimento de software baseadas na escrita prévia de testes. O TDD foca na qualidade técnica do código e testes unitários, enquanto o BDD expande essa ideia para o comportamento do sistema e a colaboração com o negócio.

Teste unitario e de compoenentes sao responsabilidades do dev
Teste de integração do especialista em testes.

Após cada integração, o desenvolvedor precisa testar os elementos afetados para garantir que eu não incluiu defeitos que não existiam

- Testes de regressão

**Tipos de manutenção: CAMP** 
1. **Corretiva:** correção de erros encontrados na verificação ou na validação.
2. **Adaptativa:** adaptação a mudansças externa.
3. **De melhoria/perfectiva:** melhorias requeridas pelos usuários.
4. **Preventiva/de reengenharia:** Abordagem pró-ativa com foco na melhoria da manutibilidade
