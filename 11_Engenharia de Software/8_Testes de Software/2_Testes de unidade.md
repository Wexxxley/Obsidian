
#Concluded 

---

Testes de unidade são t<mark style="background: #ADCCFFA6;">estes automatizados que verificam pequenas unidades de código, geralmente classes, de forma isolada</mark> do restante do sistema. Um teste de unidade é, essencialmente, um programa que chama métodos de uma classe e verifica se os resultados retornados são os esperados.    

- O código de um sistema é dividido em:
    - **Classes de produção:** Implementam os requisitos do sistema.
    - **Classes de teste:** Contêm o código que testa as classes de produção .

---
### **Frameworks xUnit**

Testes de unidade são implementados usando frameworks específicos. Os mais conhecidos são da família **xUnit**, onde 'x' indica a linguagem (JUnit, NUnit, pytest, etc.) .

**Exemplo:** A classe Stack tem métodos como `size()`, `isEmpty()`, `push()` e `pop()`, usando um `ArrayList` internamente.
```java
import java.util.ArrayList;
 import java.util.EmptyStackException;

 public class Stack<T> {
  private ArrayList<T> elements = new ArrayList<T>();
  private int size = 0;

  public int size() {
  return size;
  }

  public boolean isEmpty() {
  return (size == 0);
  }

  public void push(T elem) {
  elements.add(elem);
  size++;
  }

  public T pop() throws EmptyStackException {
  if (isEmpty())
	  throw new EmptyStackException();
	  T elem = elements.remove(size-1);
	  size--;
	  return elem;
  }
 }
```

- **Métodos de Teste:**        
    - Devem ser `public`.
    - Não podem ter parâmetros.
    - Precisam da anotação `@Test` para serem reconhecidos pelo JUnit .

```java
 import org.junit.Test;
 import static org.junit.Assert.assertTrue;

 public class StackTest {

  @Test
  public void testEmptyStack() {
   Stack<Integer> stack = new Stack<Integer>(); // 1. Setup
   boolean empty = stack.isEmpty(); // 2. Call method
   assertTrue(empty); // 3. Assert
  }

 }
```

- **Estrutura de um Método de Teste:**
    1. **Setup :** Cria o contexto, instanciando e inicializando os objetos a serem testados.
    2. **Chamada do Método:** Executa o método da classe que está sendo testado . No exemplo, `stack.isEmpty()`.
    3. **Assert:** Verifica se o resultado obtido é o esperado, usando comandos `assert` fornecidos pelo framework JUnit. Como `assertTrue`, `assertEquals`, `assertFalse`, etc.) .

---
### **Quando Escrever Testes de Unidade?**

1. **Após Implementar Pequenas Funcionalidades:** Você pode implementar alguns métodos ou uma pequena parte de uma funcionalidade e, logo em seguida, escrever os testes de unidade para ela.

<mark style="background: #ADCCFFA6;">	programar um pouco -> escrever testes -> programar mais um pouco -> escrever mais testes .</mark>

2. **Antes de Implementar o Código (TDD):** Escrever o teste _primeiro_. Ele inicialmente falhará. Em seguida, implementa-se o código de produção mínimo necessário para fazer o teste passar, e depois refatora-se o código. 

3. **Ao Corrigir um Bug:** Quando um bug é reportado, comece escrevendo um teste de unidade que reproduza o bug. Depois, corrija o bug no código de produção. Se a correção foi bem-sucedida, o teste que você escreveu passará, e ele fica na suíte de testes para evitar que o mesmo bug retorne no futuro (regressão) .

4. **Durante a Depuração:** Em vez de usar `System.out.println`  para verificar o comportamento de um método durante a depuração, escreva um teste de unidade. O `println` é temporário e será removido, enquanto o teste permanece como um ativo para a suíte de testes .

---
### **Benefícios dos Testes de Unidade**

1. **Encontrar Bugs Cedo:** Permitem detectar defeitos ainda na fase de desenvolvimento, antes que o código chegue à produção.
    
2. **Rede de Proteção Contra Regressões:** Quando você faz uma modificação no código (para corrigir um bug, adicionar funcionalidade ou refatorar), rodar a suíte de testes ajuda a garantir que sua mudança não quebrou algo que antes funcionava . 
    
3. **Documentação Viva e Especificação:** Os testes mostram como usar as classes e métodos do código de produção e qual comportamento é esperado deles . 
    

---
### **Cobertura de Testes**

Cobertura de testes é uma <mark style="background: #ADCCFFA6;">métrica que indica a quantidade do código de produção que é exercitada pela execução da suíte de testes</mark>.
    
- A definição mais comum é baseada em comandos ou linhas executáveis:
    
    $cobertura = \frac{\text{número de comandos executados pelos testes}}{\text{total de comandos do programa}}$
    
![](../../attachments/Pasted%20image%2020251027140715.png)

**Qual a Cobertura de Testes Ideal?** de 60% a 85%
