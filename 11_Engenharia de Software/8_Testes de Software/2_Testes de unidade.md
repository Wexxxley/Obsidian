
---

Testes de unidade são t<mark style="background: #ADCCFFA6;">estes automatizados que verificam pequenas unidades de código, geralmente classes, de forma isolada</mark> do restante do sistema. Um teste de unidade é, essencialmente, um programa que chama métodos de uma classe e verifica se os resultados retornados são os esperados.    

- O código de um sistema é dividido em:
    - **Classes de produção:** Implementam os requisitos do sistema.
    - **Classes de teste:** Contêm o código que testa as classes de produção .


**Frameworks xUnit:**

- Testes de unidade são implementados usando frameworks específicos. Os mais conhecidos são da família **xUnit**, onde 'x' indica a linguagem (JUnit para Java, NUnit para .NET, pytest para Python, etc.) .
    
- O primeiro foi o sUnit (para Smalltalk), criado por Kent Beck. O JUnit (para Java) foi criado por Kent Beck e Erich Gamma em 1997 .
    
- Uma vantagem é que os testes são escritos na **mesma linguagem** do sistema, facilitando para os desenvolvedores.
    

**Exemplo: Classe `Stack`** O livro usa uma classe `Stack` simples em Java como exemplo para testes . Ela tem métodos como `size()`, `isEmpty()`, `push()` e `pop()`, usando um `ArrayList` internamente.

**Exemplo: Classe `StackTest` (JUnit)**

- **Convenção de Nomenclatura:** Classes de teste geralmente têm o mesmo nome da classe testada, com sufixo `Test` (ex: `StackTest`) .
    
- **Métodos de Teste:**
    
    - Começam com o prefixo `test` (convenção antiga, hoje a anotação `@Test` é suficiente).
        
    - Devem ser `public`.
        
    - Não podem ter parâmetros.
        
    - Precisam da anotação `@Test` para serem reconhecidos pelo JUnit .
        

**Primeiro Teste Simples:**

Java

```
 import org.junit.Test;
 import static org.junit.Assert.assertTrue;

 public class StackTest {

  @Test
  public void testEmptyStack() {
   Stack<Integer> stack = new Stack<Integer>(); // 1. Setup (Fixture)
   boolean empty = stack.isEmpty(); // 2. Call method
   assertTrue(empty); // 3. Assert
  }

 }
```

- **Estrutura de um Método de Teste:**
    
    1. **Setup (Fixture):** Cria o contexto, instanciando e inicializando os objetos a serem testados . No exemplo, `new Stack<Integer>()`.
        
    2. **Chamada do Método:** Executa o método da classe que está sendo testado . No exemplo, `stack.isEmpty()`.
        
    3. **Assert:** Verifica se o resultado obtido é o esperado, usando comandos `assert` fornecidos pelo framework JUnit (como `assertTrue`, `assertEquals`, `assertFalse`, etc.) .
        

**Execução e Resultados:**

- IDEs permitem rodar os testes separadamente da execução normal do programa (opção "Run as Test") .
    
- O resultado é visual:
    
    - **Barra Verde:** Todos os testes passaram.
        
    - **Barra Vermelha:** Pelo menos um teste falhou.
        
- Testes de unidade são rápidos (ex: 0.025 segundos no exemplo).
    
- **Falha (Failure):** Ocorre quando um `assert` não é satisfeito . A IDE indica qual teste e qual linha do `assert` falhou.
    

**Exemplo Completo `StackTest`:** O livro apresenta uma versão mais completa com:

- **`@Before`:** Uma anotação para um método (ex: `init()`) que o JUnit executa _antes_ de _cada_ método `@Test` naquela classe . Útil para inicializar objetos comuns a vários testes (como a `stack`) .
    
- **Múltiplos `@Test`:** Cada um foca em um aspecto diferente (`testNotEmptyStack`, `testSizeStack`, `testPushPopStack`).
    
- **Diferentes `Asserts`:** `assertFalse`, `assertEquals(expected, actual)`.
    
- **Teste de Exceções:** Para testar se uma exceção esperada é lançada, usa-se um parâmetro na anotação `@Test`: `@Test(expected = ExpectedException.class)`. O teste passa _se_ a exceção especificada for lançada durante a execução do método . Não se usa `assert` nesses casos, pois a exceção interromperia o fluxo antes do `assert`.
    

**Fluxo de Execução do JUnit:** Para cada classe de teste, o JUnit:

1. Para cada método `@Test` `m`:
    
2. Cria uma _nova instância_ da classe de teste .
    
3. Se houver um método `@Before` `b`, executa `b` nessa instância .
    
4. Executa o método `@Test` `m` nessa instância.
    

**Definições Importantes:**

- **Teste (Test):** O método anotado com `@Test` .
    
- **Fixture:** O estado (objetos, dados) preparado para a execução de um ou mais testes .
    
- **Caso de Teste (Test Case):** A classe que contém os métodos de teste .
    
- **Suíte de Testes (Test Suite):** Um conjunto de casos de teste executados juntos.
    
- **Sistema sob Teste (System Under Test - SUT):** O código (classe, método) que está sendo testado; também chamado de código de produção .
    

Terminamos os conceitos básicos de Testes de Unidade. Digite "next" para passarmos às seções sobre quando escrever testes e seus benefícios.