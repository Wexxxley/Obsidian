

---

Testes são fundamentais para evitar que esses erros cheguem aos usuários finais e causem prejuízos. Testar é uma das práticas de programação mais valorizadas atualmente.

### **Evolução das Práticas de Teste**

- **Modelo Waterfall (Tradicional):**
    - Testes ocorriam em uma fase separada, _após_ a codificação.
    - Frequentemente realizados por uma equipe de testes separada.
    - Muitas vezes manuais (alguém usava o sistema e verificava as saídas).
    - O objetivo principal era apenas detectar bugs antes da produção.
        
- **Métodos Ágeis (Moderno):**
    
    - Grande parte dos testes passou a ser **automatizada** (código testa código) .
        
    - Testes são escritos **durante** o desenvolvimento, às vezes até _antes_ do código de produção.
        
    - O **próprio desenvolvedor** que implementa a classe também implementa seus testes.
        
    - Testes ganharam **novas funções**: além de detectar bugs, servem como **rede de proteção contra regressões** (garantir que mudanças não quebrem o que funcionava) e como **documentação** do código .
        

**Foco do Capítulo:**

- O capítulo focará em **testes automatizados**, pois os manuais são trabalhosos, demorados, caros e precisam ser repetidos a cada modificação .
    

**A Pirâmide de Testes (Mike Cohn):**

- Classifica os testes automatizados pela granularidade :
    
    1. **Testes de Unidade (Base da Pirâmide):**
        
        - Verificam pequenas partes isoladas do código (geralmente uma classe) .
            
        - São os mais numerosos (formam a base).
            
        - Simples, fáceis de implementar e rápidos de executar.
            
    2. **Testes de Integração (ou de Serviços) (Meio da Pirâmide):**
        
        - Verificam uma funcionalidade ou transação completa, envolvendo diversas classes e, possivelmente, componentes externos (banco de dados, outros serviços) .
            
        - Demandam mais esforço e executam mais lentamente.
            
    3. **Testes de Sistema (ou de Interface/Ponta-a-Ponta) (Topo da Pirâmide):**
        
        - Simulam a interação de um usuário real com o sistema através de sua interface .
            
        - São os mais caros, mais lentos e menos numerosos .
            
        - Costumam ser frágeis (pequenas mudanças na interface podem quebrá-los).
            
- **Proporção Recomendada:** Aproximadamente 70% Unidade, 20% Integração, 10% Sistema. O capítulo seguirá essa proporção na profundidade da abordagem .
    

**Relembrando Conceitos:**

- **Defeito/Bug:** Código que não está de acordo com sua especificação.
    
- **Falha (Failure):** Resultado ou comportamento incorreto exibido quando um código com defeito é executado.
    

Terminamos a introdução. Quando estiver pronto, digite "next" para começarmos a detalhar os Testes de Unidade.