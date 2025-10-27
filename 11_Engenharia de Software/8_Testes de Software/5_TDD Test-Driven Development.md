
#Concluded 

---

O TDD (Desenvolvimento Dirigido por Testes) é uma das práticas de programação propostas originalmente por Extreme Programming (XP) .

**O Fluxo Básico de TDD:**

1. **Escrever um Teste :** Comece escrevendo um teste automatizado para uma pequena funcionalidade que você deseja implementar. Como o código de produção ainda não existe, esse teste **deve falhar** inicialmente.
    
2. **Escrever o Código Mínimo:** Escreva a quantidade **mínima** de código de produção necessária para fazer o teste que você acabou de escrever passar.
    
3. **Refatorar:** Com o teste passando, agora você pode melhorar (refatorar) tanto o código de produção quanto o código do teste, garantindo que os testes continuem passando.

**Objetivos Principais do TDD:** TDD não é apenas sobre testar, mas também sobre design e disciplina. Seus principais objetivos são:

1. **Garantir que os Testes Sejam Escritos:** Ao tornar a escrita do teste a _primeira_ atividade, TDD evita que os testes sejam esquecidos ou deixados para depois .
    
2. **Promover Código com Alta Testabilidade:** Como o desenvolvedor escreve o teste _antes_ do código, ele naturalmente pensa em como tornar o código testável desde o início. Isso geralmente leva a designs mais desacoplados e com maior cobertura de testes (frequentemente > 90%) .
    
3. **Melhorar o Design do Código:** Ao escrever o teste primeiro, o desenvolvedor se coloca na posição de _usuário_ da classe/método que será implementado. Isso o incentiva a pensar na interface (API) da classe, buscando simplicidade, nomes claros, poucos parâmetros, etc., o que leva a um design melhor e mais fácil de usar .
    

**O Ciclo Red-Green-Refactor:** O fluxo de trabalho TDD é frequentemente descrito como um ciclo com três fases ou estados:

1. **RED (Vermelho):**
    
    - Escreva um pequeno teste que falha.
        
    - O objetivo é definir o que você quer implementar e qual será a interface. Ter um teste falhando já é um progresso, pois define o próximo passo .
        
    - O código deve pelo menos compilar (pode ser necessário criar esqueletos de classes/métodos) .
        
2. **GREEN (Verde):**
    
    - Escreva o código de produção **mais simples possível** para fazer o teste passar.
        
    - Pode até ser um código "forçado" inicialmente (ex: retornar uma constante) apenas para sair do vermelho rapidamente (baby steps) . Depois, implementa-se a lógica correta.
        
3. **REFACTOR (Amarelo/Refatoração):**
    
    - Com o teste passando, olhe para o código (tanto de produção quanto de teste) e veja se há oportunidades de melhorá-lo: remover duplicação, melhorar nomes, simplificar a lógica, aplicar princípios de design, etc. .
        
    - Execute os testes novamente após a refatoração para garantir que nada foi quebrado.
        
    - Após refatorar, o ciclo recomeça: escreve-se um novo teste que falha para a próxima pequena funcionalidade.