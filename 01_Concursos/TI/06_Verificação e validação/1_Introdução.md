

---

Clientes frequentemente expressam necessidades de negócio propondo soluções. O cliente relata os sintomas de um processo falho e, instintivamente, tenta formular uma resolução com base no seu próprio conhecimento empírico sobre tecnologia, o qual geralmente é limitado.

### A Investigação da Causa Raiz

A engenharia de requisitos exige que o profissional não atue como um mero anotador de pedidos. É necessário aplicar técnicas de **elicitação** (o processo técnico de coleta, extração e descoberta de informações) para isolar a causa fundamental do problema. O objetivo primário é compreender a dor do processo de negócio, descartando as restrições artificiais impostas pela sugestão técnica inicial do cliente.

### Separação de Domínios

Para encontrar a solução ideal, a análise de software divide o projeto em duas áreas estritamente separadas:

- **Domínio do Problema:** O ambiente de negócio do cliente, as regras operacionais, os gargalos e as restrições financeiras ou de tempo. É o cenário onde a necessidade real reside.
    
- **Domínio da Solução:** A arquitetura de software, as linguagens de programação, os bancos de dados e as interfaces projetadas.
    

O analista deve esgotar e mapear completamente o domínio do problema antes de permitir que a equipe de engenharia inicie o desenvolvimento do domínio d

No máximo vc pode aumentar a probabilidade de alguém n encontrar um erro.
![500](../../../attachments/Pasted%20image%2020260814082942.png)

O **TDD** (_Test-Driven Development_) e o **BDD** (_Behavior-Driven Development_) são práticas de desenvolvimento de software baseadas na escrita prévia de testes. O TDD foca na qualidade técnica do código e testes unitários, enquanto o BDD expande essa ideia para o comportamento do sistema e a colaboração com o negócio.


Teste unitario e de compoenentes sao responsabilidades do dev
Teste de integração do especialista em testes.

Após cada integração, o desenvolvedor precisa testar os elementos afetados para garantir que eu não incluiu defeitos que não existiam

- Testes de regressão


**Validação**: é voltar ao doc de requisitos /cliente e ver se o que foi feito é o que ele queria, o que foi proposto, se ele valida.

**Verificação**: n é se eu entedi direito, é se o que construi n quebra, se n tem bug, se é robusto.
- **Estática/Inspeções de software:** n executa codigo. pode ser inclusive no doc de requisitos. linhas duplicadas, var n usados, metodos que fz mais de uma coisa. codes semels. 
- **Dinamica/testes de software:** codigo executado. Verifica se o comportamento é o esperado.

- Inspeção é uma revisão cuidadosa, linha por linha, do código fonte do programa.
-  Inspeções não podem verificar as características não funcionais tais como desempenho, usabilidade, etc.
- Objetivo é a DETECÇÃO de defeitos (não correção). Defeitos podem ser erros lógicos, anomalias no código que podem indicar uma condição errônea ou a não conformidade com padrões organizacionais


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
