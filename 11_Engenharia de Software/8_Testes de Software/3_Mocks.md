

---

Obs: O livro menciona que, inicialmente, usará os termos **mock** e **stub** como sinônimos, mas que há uma distinção mais sutil que será abordada posteriormente.

Imagine uma classe `BookSearch` que busca informações de livros. Ela depende de uma interface `BookService`, que representa um serviço externo para obter os dados do livro, retornando-os como uma string JSON. O método `getBook` da classe `BookSearch` chama o serviço externo, recebe o JSON e o converte (parse) em um objeto `Book` .

```java
 import org.json.JSONObject;

 public class BookSearch {

  BookService rbs; // Dependência externa

  public BookSearch(BookService rbs) {
	  this.rbs = rbs;
  }

  public Book getBook(int isbn) {
	  String json = rbs.search(isbn); // Chama o serviço externo
	  JSONObject obj = new JSONObject(json);
	  String titulo = (String) obj.get("titulo");
	  return new Book(titulo); // Cria o objeto Book
  }
 }

 public interface BookService {
  String search(int isbn); // Método que acessa o sistema externo
 }
```

**O Problema para Testes de Unidade:**

- Queremos testar a classe `BookSearch`, especificamente a lógica dentro do método `getBook` (o parse do JSON e a criação do objeto `Book`).
    
- No entanto, `getBook` **depende** do `BookService`, que é um serviço externo.
    
- Chamar o serviço externo _real_ dentro de um teste de unidade é **ruim** porque 5:
    
    - O teste deixa de ser de _unidade_ (testaria `BookSearch` + `BookService`).
        
    - O teste fica **lento** (depende de rede ou acesso a disco).
        
    - O teste fica **não determinístico / frágil** (pode falhar se a rede estiver fora, o serviço externo estiver indisponível ou os dados externos mudarem).
        
    - Viola o princípio FIRST (testes devem ser Rápidos e Independentes).
        

**A Solução: Usar Mocks (ou Stubs)**

- Criamos uma **implementação "falsa"** da dependência (`BookService`), chamada de **mock** (ou stub) 6.
    
- Essa implementação falsa **simula** o comportamento da dependência real, mas de forma controlada e previsível, **sem acessar o sistema externo**.
    
- Ela retorna dados pré-definidos que são necessários para o teste.
    

**Exemplo de Mock Manual (`MockBookService`):**

Java

```
 class BookConst { // Constantes para JSONs de teste
  public static String ESM =
  "{ \"titulo\": \"Eng Soft Moderna\" }";
  public static String NULLBOOK =
  "{ \"titulo\": \"NULL\" }";
 }

 class MockBookService implements BookService { // Implementação Mock

  // Simula o search, retornando JSON fixo para ISBN 1234
  public String search(int isbn) {
  if (isbn == 1234)
  return BookConst.ESM;
  return BookConst.NULLBOOK;
  }

 }
```

- `MockBookService` implementa `BookService`.
    
- Seu método `search` não acessa nenhum serviço externo; ele apenas retorna uma string JSON fixa se o ISBN for 1234, e outra string caso contrário.
    

**Exemplo de Teste de Unidade Usando o Mock:**

Java

```
 import static org.junit.Assert.*;
 import org.junit.*;

 public class BookSearchTest {

  private BookService service; // Vai receber o Mock

  @Before
  public void init() {
  service = new MockBookService(); // Instancia o Mock
  }

  @Test
  public void testGetBook() {
  // Injeta o Mock na classe sob teste
  BookSearch bs = new BookSearch(service);
  // Executa o método a ser testado
  String titulo = bs.getBook(1234).getTitulo();
  // Verifica se o parse do JSON (retornado pelo Mock) foi correto
  assertEquals("Eng Soft Moderna", titulo);
  }

 }
```

- No método `@Before`, criamos uma instância do **mock** (`MockBookService`).
    
- No teste `testGetBook`, criamos a instância de `BookSearch` **injetando o mock** no construtor.
    
- Quando `bs.getBook(1234)` é chamado, ele internamente chama `service.search(1234)`. Como `service` é o mock, ele retorna o JSON `"{"titulo": "Eng Soft Moderna"}"` **imediatamente**, sem ir à rede.
    
- O `assert` então verifica se `BookSearch` conseguiu parsear corretamente esse JSON específico e extrair o título "Eng Soft Moderna".
    

**O que o Teste Realmente Verifica?**

- Este teste **NÃO** verifica se o serviço externo (`BookService`) está funcionando corretamente.
    
- Ele verifica **APENAS** a lógica _dentro_ da classe `BookSearch`: se ela chama corretamente o método `search` da dependência e se ela consegue processar (parsear) a resposta JSON esperada e criar o objeto `Book` adequadamente 7.
    

Mocks são essenciais para isolar a unidade sob teste de suas dependências, permitindo testes de unidade verdadeiros (rápidos, independentes, determinísticos).

Terminamos a introdução aos mocks com um exemplo manual. Digite "next" para vermos como frameworks podem facilitar a criação de mocks.