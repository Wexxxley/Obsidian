
#Concluded 

---
### **Princípios FIRST** 

<mark style="background: #BBFABBA6;">Fast, Independent, Repeatable, Self-checking, Timely</mark>

Testes de unidade de boa qualidade devem satisfazer às seguintes propriedades:

- **Rápidos (Fast):**
    - Testes de unidade devem executar muito rapidamente. Isso permite que os desenvolvedores os executem com frequência (várias vezes ao dia) para obter feedback rápido sobre o código que estão escrevendo ou modificando.
        
- **Independentes (Independent):**
    - A ordem de execução dos testes **não** deve importar. O resultado de um teste não pode depender de outro teste ter sido executado antes.
    - Cada teste deve configurar seu próprio ambiente (fixture) e não deixar "sujeira" (estados alterados) que possa afetar outros testes.
        
- **Repetíveis (Repeatable): **
    - Um teste deve produzir **sempre o mesmo resultado** (passar ou falhar) cada vez que é executado, desde que o código de produção não tenha mudado .
        
- **Auto-verificáveis (Self-checking): **
    - O teste deve ser capaz de determinar automaticamente se passou ou falhou, sem intervenção manual (como inspecionar saídas no console ou em arquivos).
        
- **Escritos o quanto antes(Timely):**
    - Os testes devem ser escritos **junto com** o código de produção ou, idealmente, **um pouco antes** (como no TDD).
    - Escrever testes tardiamente aumenta o risco de não serem escritos ou de serem de baixa qualidade.
        
---
### **Test Smells**

São sinais de problemas potenciais no código dos testes, indicando que eles podem ser difíceis de entender ou manter. 

- **Teste Obscuro:**
    - Um teste muito longo, complexo ou difícil de entender.
        
- **Teste com Lógica Condicional :**
    - O teste contém comandos `if`, `switch`, `for`, `while`. Isso torna o teste mais difícil de entender e pode fazer com que diferentes execuções do mesmo teste sigam caminhos distintos, ou que partes do teste não sejam executadas. Testes devem ser, idealmente, lineares.
        
- **Duplicação de Código em Testes:**
    - Código repetido em vários métodos de teste (ex: código de setup/fixture).
    - Pode ser resolvido usando métodos `@Before` ou métodos auxiliares privados dentro da classe de teste.
        
