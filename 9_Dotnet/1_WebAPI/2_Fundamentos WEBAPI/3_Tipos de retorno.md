
#Concluded 

---
### **1. Retornos síncronos**
Os endpoints possuem três tipos de retornos, que são:
- **Tipo específico**: Como string, int, struct, class, etc. Não é recomendado, pois impossibilita o retorno de códigos de status HTTP.
- **IActionResult**: Permite o retorno de código status HTTP, mas não de tipos específicos sozinhos.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeshwbmN1PQLOspPud4unpA8vQwl_iX_4TSHvwzt2DWW_v36kOZSJL1mveia3UhxtkDJUbPT0y6S3luBHOWv0jkV3tocLT_HgW0kBqkAQbTQA9k5cRpd34JZKUC-e9t1C7GNpfFLCW3XJ1rLh8aqhJINgKZ?key=SZHaDLu24DLXyFgiFaRNLA)
Note que não é possível retornar somente o product.
- ``ActionResult<T>``: Possibilita o retorno de código de status e tipos específicos
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf8w6Bh8pP5v1I2lRxBxqOTUgTDqF1tQLLYegeOhYaxiO-6gOrM3xbD21yiTEr79HwJmFfwTBr3DDPimcL_JRMrNfaTJhlmUTwiy7qatIMHj5o7Hdch4k5m2bcqmEauXhVgfkO12YS8c6ek782hEd5Cm0A?key=SZHaDLu24DLXyFgiFaRNLA)

---
### **2. Retornos assíncronos**
Quando uma ação do controller precisa executar uma operação que pode demorar, como uma consulta ao banco de dados ou uma chamada a outra API, usamos programação assíncrona para não bloquear o servidor.

Quando um método é marcado como `async`, seu tipo de retorno **obrigatoriamente** precisa ser encapsulado em um `Task`. A lógica é uma correspondência direta dos tipos síncronos:

- **`Task<T>`**: Versão assíncrona do `T`. Representa uma operação futura que, quando concluída, retornará um objeto do tipo `T`. Assim como a versão síncrona, não é o mais recomendado por não permitir o retorno de códigos de status HTTP de forma flexível.
- **`Task<IActionResult>`**: Versão assíncrona do `IActionResult`. É usado quando a ação realiza operações `await` e precisa retornar diferentes resultados baseados em `IActionResult` (como `Ok()`, `NotFound()`, `BadRequest()`).
- **`Task<ActionResult<T>>`**: Versão assíncrona do `ActionResult<T>`. É a opção mais completa e recomendada para a maioria dos casos em APIs modernas. Permite que você realize operações `await` e retorne tanto códigos de status HTTP quanto um tipo de dado específico.
