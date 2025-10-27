
#Concluded 

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

Queremos testar a classe `BookSearch`, especificamente a lógica dentro do método `getBook`. No entanto, `getBook` **depende** do `BookService`, que é um serviço externo.

Chamar o serviço externo _real_ dentro de um teste de unidade é **ruim** porque:
- O teste deixa de ser de _unidade_.
- O teste fica **lento**.
- O teste fica **não determinístico / frágil** (pode falhar se a rede estiver fora, o serviço externo estiver indisponível ou os dados externos mudarem).

---
### **A Solução: Usar Mocks**

Criamos uma **implementação "falsa"** da dependência (`BookService`), chamada de mock. Essa implementação falsa **simula** o comportamento da dependência real, mas de forma controlada e previsível, **sem acessar o sistema externo**. Ela retorna dados pré-definidos que são necessários para o teste.

**Exemplo de Mock Manual (`MockBookService`):**

```java
 class BookConst { // Constantes para JSONs de teste
	  public static String ESM =
	  "{ \"titulo\": \"Eng Soft Moderna\" }";
	  public static String NULLBOOK =
	  "{ \"titulo\": \"NULL\" }";
 }

 class MockBookService implements BookService { // Implementação Mock
	  public String search(int isbn) {
	  if (isbn == 1234)
	  return BookConst.ESM;
	  return BookConst.NULLBOOK;
	  }
 }
```

Mocks são essenciais para isolar a unidade sob teste de suas dependências, permitindo testes de unidade verdadeiros (rápidos, independentes, determinísticos).
