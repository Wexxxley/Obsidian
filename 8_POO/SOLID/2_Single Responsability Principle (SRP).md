
“Uma classe deve ter apenas um motivo para mudar.”

 Se uma classe tem **mais de uma responsabilidade**, as **responsabilidades se tornam acopladas**. Mudanças em uma responsabilidade podem prejudicar a capacidade da classe de cumprir as outras. Outra forma de entender SRP é: uma classe tem que se preocupar em responder somente a um grupo de atores.

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
```java
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
- **Depois:** Se o salvamento falhar, você sabe **imediatamente** que o erro está na classe **`OrderRepository`**.

**Facilidade de Testes Unitários** 
- **Antes:** Para testar se o cálculo do preço estava correto, seu teste teria que interagir com o banco de dados e possivelmente tentar enviar um e-mail. Isso não é um teste unitário puro.
- **Depois:** Para testar a **`OrderProcessor`**, você pode **simular (_mock_)** o banco de dados e o serviço de e-mail. O teste foca apenas em garantir que a `OrderProcessor` **chame** os métodos corretos, sem realmente salvar ou enviar.

**Manutenção e Flexibilidade** 
- **Antes:** Se você mudar a forma como o e-mail é enviado, você teria que abrir e modificar a classe `OrderProcessor`, quebrando o código que lida com o banco de dados e o cálculo.
- **Depois:** Se você mudar o banco de dados você só precisa modificar a classe **`OrderRepository`.** As classes **`OrderCalculator`** e **`EmailService`** permanecem totalmente intactas.
