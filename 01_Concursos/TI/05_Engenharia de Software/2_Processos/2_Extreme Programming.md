
#Concluded 

---
Sendo um **método ágil**, XP possui todas as características dos processos agéis, isto é: adota **ciclos curtos** e iterativos de desenvolvimento, concede **menos ênfase para documentação**, propõe que o design de um sistema também seja definido de forma incremental e sugere que as equipes de desenvolvimento sejam pequenas.

XP não é um método prescritivo. Em vez disso, <mark style="background: #ADCCFFA6;">XP é definido por meio de um conjunto de valores, princípios e práticas de desenvolvimento. Ou seja, XP é definido de forma abstrata. </mark>

---
### 1. Valores e Princípios

Os **Valores** são a base cultural do XP. Os principais são:

- Comunicação    
- Simplicidade
- Feedback
- Coragem
- Respeito
- Qualidade de Vida

---
### 2. Práticas do XP

#### 2.1 Práticas sobre o Processo de Desenvolvimento

- **Representante dos Clientes:** Um representante do cliente trabalha junto com o time de desenvolvimento, em tempo integral, para escrever histórias e tirar dúvidas .
    
- **Histórias de Usuários :** Requisitos escritos em linguagem simples pelo cliente .
    
- **Iterações:** Ciclos de trabalho curtos (1 a 3 semanas).
    
- **Releases:** Ciclos mais longos (2 a 3 meses) compostos por várias iterações.
    
- **Planning Poker:** Técnica de estimativa em grupo para definir o tamanho das histórias .
    
- **Slack (Folga):** Adicionar tarefas de baixa prioridade (ou tempo de estudo) no planejamento da iteração. 
    
#### 2.2 Práticas de Programação

- **Design Incremental:** O design (arquitetura) do sistema evolui a cada iteração, em vez de ser definido completamente no início (sem "Big Design Up Front").
    
- **Pair Programming:** Técnica onde o código é escrito por **dois desenvolvedores** trabalhando juntos no mesmo computador.
    
- **TDD (Desenvolvimento Dirigido por Testes):** A prática de **escrever os testes de unidade _antes_** de escrever o código de produção que faz o teste passar .
    
- **Build Automatizado:** O processo de compilar o sistema e rodar os testes deve ser totalmente automatizado e rápido.
    
- **Integração Contínua (CI):** Os desenvolvedores devem integrar seu código no _branch_ principal (master/trunk) frequentemente, pelo menos uma vez por dia .
    
- **Propriedade Coletiva do Código:** Qualquer desenvolvedor da equipe pode alterar qualquer parte do código do sistema a qualquer momento, sem pedir permissão ao "dono" original .
    
#### 2.3 Práticas de Gerenciamento de Projetos

- **Ambiente de Trabalho:** O time deve ser pequeno, dedicado 100% ao projeto e, idealmente, trabalhar na mesma sala para facilitar a comunicação .
    
- **Jornadas de Trabalho Sustentáveis:** A equipe deve trabalhar em ritmo sustentável (ex: 40 horas semanais) e evitar horas extras excessivas, que levam à exaustão e queda de qualidade .
    
- **Contratos com Escopo Aberto:** O XP prefere contratos onde o cliente paga por hora/iteração, permitindo que ele mude os requisitos (o escopo) ao longo do projeto, em vez de contratos de escopo fechado.

---
## Planning Poker.  

Planning Poker é uma técnica usada para estimar o tamanho das Histórias de Usuário.

1. **Apresentação**: Representante dos clientes seleciona uma história e a lê para os devs.
    
2. **Esclarecimento**: Os desenvolvedores tiram suas dúvidas sobre a história diretamente com o representante dos clientes para entendê-la melhor.
    
3. **Estimativa Individual:** Cada desenvolvedor faz sua estimativa independente para o tamanho da história.
    
4. **Revelação Simultânea**: Todos os desenvolvedores, ao mesmo tempo, levantam cartões mostrando a estimativa que pensaram.
    
5. **Verificação de consenso**: Se houver consenso o tamanho da história está estimado e o time passa para a próxima. Se não houver consenso o time inicia uma discussão.
    
6. **Discussão**: Os desenvolvedores com as estimativas mais discrepantes explicam o porquê de suas propostas.
    
7. **Repetição**: Após a discussão, o time realiza uma nova votação.



