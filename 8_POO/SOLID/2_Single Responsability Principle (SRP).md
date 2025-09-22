
---
==“Uma classe deve ter apenas um motivo para mudar.”==

 Se uma classe tem **mais de uma responsabilidade**, as **responsabilidades se tornam acopladas**. Mudanças em uma responsabilidade podem prejudicar a capacidade da classe de cumprir as outras. Outra forma de entender SRP é: ==uma classe tem que se preocupar em responder somente a um grupo de atores.==

**Exemplo**
```c#
public class OrderProcessor  
{  
	public void ProcessOrder(Order order)  
	{  
	// Calculate total price  
	order.TotalPrice = order.Items.Sum(item => item.Price * item.Quantity);  
	  
	// Save order to database  
	SaveToDatabase(order);  
	  
	// Send confirmation email  
	Console.WriteLine($"Email sent to {order.CustomerEmail}.");  
	  
	private void SaveToDatabase(Order order)  
	{  
		Console.WriteLine($"Order saved");  
	}  
}  
```

OrderProcessor tem 3 responsabilidadess diferentes:
1. Calculating total price
2. Saving the order to database
3. Sending confirmation email

**Refatorando**
```c#
public class OrderProcessor  
{  
	private readonly OrderCalculator _orderCalculator;  
	private readonly OrderRepository _orderRepository;  
	private readonly EmailService _emailService;  
	  
	public OrderProcessor()  
	{  
		_orderCalculator = new OrderCalculator();  
		_orderRepository = new OrderRepository();  
		_emailService = new EmailService();  
	}  
	  
	public void ProcessOrder(Order order)  
	{  
		// Calculate total price  
		_orderCalculator.CalculateTotal(order);  
		  
		// Save order to database  
		_orderRepository.Save(order);  
		  
		// Send confirmation email  
		_emailService.SendConfirmation(order.CustomerEmail);  
	}  
}  
  
public class OrderCalculator  
{  
	public void CalculateTotal(Order order)  {  
		order.TotalPrice = order.Items.Sum(item => item.Price * quantity);  
	}  
}  
  
public class OrderRepository  
{  
	public void Save(Order order)  
	{  
		Console.WriteLine($"Order saved"); 
	}  
}  
  
public class EmailService  
	{  
	public void SendConfirmation(string email)  
	{  
		Console.WriteLine($"Email sent to {email}");  
	}  
}  
```

O que foi feito:
- Uso de uma classe separada, **`OrderCalculator`**, para calcular o valor total do pedido.
- Uso da classe de repositório, **`OrderRepository`**, para cuidar da comunicação com o db.
- Uso da classe de serviço, **`EmailService`**, para enviar o e-mail de confirmação do pedido.


**Localização Rápida de Erros**
- **Antes:** Se o cálculo do preço estivesse errado, o e-mail não fosse enviado, ou o salvamento falhasse, você procuraria o erro em uma única e grande classe, a `OrderProcessor`.
- **Depois:** Se o salvamento falhar, você sabe **imediatamente** que o erro está na classe **`OrderRepository`**. Se o preço estiver errado, o problema está na **`OrderCalculator`**. Isso economiza horas de depuração (_debugging_).
    

---

## 2. Facilidade de Testes Unitários (Unit Testing) ✅

- **Antes:** Para testar se o cálculo do preço estava correto, seu teste teria que interagir com o banco de dados e possivelmente tentar enviar um e-mail. Isso não é um teste unitário puro.
    
- **Depois:** Para testar a **`OrderProcessor`**, você pode **simular (_mock_)** o banco de dados e o serviço de e-mail. O teste foca apenas em garantir que a `OrderProcessor` **chame** os métodos corretos, sem realmente salvar ou enviar.
    

---

## 3. Manutenção e Flexibilidade (Manutenibilidade) 🛠️

- **Antes:** Se você mudar a forma como o e-mail é enviado (por exemplo, de `Console.WriteLine` para um serviço como SendGrid), você teria que abrir e modificar a classe `OrderProcessor`, quebrando o código que lida com o banco de dados e o cálculo.
    
- **Depois:** Se você mudar o banco de dados (por exemplo, de SQL para NoSQL), você só precisa modificar a classe **`OrderRepository`**. As classes **`OrderCalculator`** e **`EmailService`** permanecem totalmente intactas e funcionando.

___________________________________________________________________________

## 1.2 Open Close Principle (OCP)

“As entidades de software (classes, módulos, funções) devem ser abertas para

ampliação, mas fechadas para modificação”.

  

 Quando uma única mudança em um programa resulta em uma sucessão de mudanças nos módulos dependentes, o projeto tem um grande problema. O OCP nos aconselha a refatorar o sistema para que alterações não causem mais modificações. Se o OCP for bem aplicado, mudanças são obtidas pela adição de novo código e não pela alteração de código antigo que já funciona. 

  

Os módulos que obedecem ao OCP têm duas características principais:

1. São abertos para ampliação: À medida que os requisitos do aplicativo mudam, podemos ampliar o módulo com novos comportamentos que satisfaçam essas alterações. 
    
2. São fechados para modificação: Ampliar o comportamento de um módulo não resulta em mudanças no código-fonte. 
    

  

 Como é possível modificar os comportamentos de um módulo sem alterar seu códi-

go-fonte?  A resposta é: com abstração. Em C# ou em qualquer outra linguagem de programação orientada a objetos, é possível criar abstrações fixas e que ainda assim representam um grupo ilimitado de comportamentos possíveis. As abstrações são classes base abstratas e o grupo ilimitado de comportamentos possíveis é representado por todas as classes derivadas possíveis.

  

 Um módulo pode manipular uma abstração. Tal módulo pode ser fechado para modificação, pois ele depende de uma abstração fixa. Apesar disso, o comportamento desse módulo pode ser ampliado pela criação de novas derivadas da abstração.

  
  
  
  
  
  
  
  
  
  
  
  
  

___________________________________________________________________________

## 1.3 Liskov Substitution Principle

“Se S é uma subclasse de T, então objetos do tipo T podem ser substituídos por objetos do tipo S sem alterar o funcionamento do programa”.

  

 Classes derivadas devem manter o comportamento esperado da classe base. Ou seja, classes derivadas não devem invalidar funcionalidades da classe base.

 No exemplo abaixo a classe abstrata Shape pode ser substituída por qualquer uma das subclasses. Elas estão implementando o método abstrato Área e todas precisam desta funcionalidade.

 O LSP evita heranças erradas que adicionam comportamentos inesperados. E se uma subclasse não consegue cumprir o contrato da classe base, a modelagem deve ser revisada.

  
  
  
  

___________________________________________________________________________

## 1.4 Interface Segregation Principle (ISP)

 O ISP diz que uma classe não deve ser forçada a implementar métodos que ela não utiliza. Isso significa que devemos criar interfaces mais específicas e enxutas, em vez de uma única interface gigante que obrigue as classes a implementar métodos irrelevantes para elas.

  

No exemplo temos uma interface IEmployee.

FullTimeEmployee utiliza e precisa de todos os métodos estabelecidos.

ContractEmployee não recebe benefícios, então não deveria ser preciso implementar o método.

  

 Para corrigir, podemos criar interfaces para FullTimeEmployee e ContractEmployee, para que essas classes não tenham que implementar métodos desnecessários.

  
  
  
  
  
  

___________________________________________________________________________

## 1.5 Dependency Inversion Principle (DIP)

 Esse princípio diz que uma classe não deve depender de implementações de outras classes, mas sim de abstrações/interfaces/contratos. Com isso temos como benefício o desacoplamento, pois é fácil trocar implementações sem impactar o código. Outra vantagem é a facilidade para testar, uma vez que podemos simular um cenário sem depender da implementação real. 

 Por exemplo, vamos supor que nosso sistema dependa de um repositório. Esse repositório pode ser um real ou uma interface. A vantagem da interface é que a implementação e o database utilizado não importa.

  

 No exemplo, PedidoService não depende da implementação de um repositório, mas sim de uma interface.

  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

Busca Binária

 A busca binária é uma forma eficiente de procurar um elemento em uma lista ordenada. Ela funciona reduzindo o espaço de busca pela metade a cada passo, em vez de olhar elemento por elemento como na busca linear.

1. Requisitos: A lista deve estar ordenada.
    
2. Passo a passo:
    

3. Escolha o elemento do meio da lista.
    
4. Compare o elemento do meio com o valor que você está procurando:
    

- Se for igual, você encontrou o que queria
    
- Se for menor, procure na parte esquerda.
    
- Se for maior, procure na parte direita.
    

3. Repita o processo apenas na metade escolhida até encontrar o valor ou até que não haja mais elementos para verificar.
    

  

Merge Sort

 O Merge Sort é um algoritmo de ordenação que segue a estratégia de Divisão e Conquista. Isso significa que ele divide o problema em partes menores, resolve essas partes, e depois mescla os resultados.

1. Dividir: Pegue o conjunto de números, e divida-o em duas partes. Continue dividindo até que cada sublista tenha um único elemento (listas com um elemento já estão ordenadas por natureza).
    
2. Conquistar: Agora comece a mesclar essas sublistas. Ao juntar duas sublistas, organize os números de cada uma de forma crescente.
    
3. Combinar: Repita o processo de mesclagem até que todas as partes estejam reunidas novamente, resultando em uma lista completamente ordenada.
    

  
**