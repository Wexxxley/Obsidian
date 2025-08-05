
#Concluded 

---
O EF Core atua como um mapeador objeto-relacional (ORM), comunicando-se com o banco de dados para você e mapeando as respostas do banco de dados para classes e objetos do .NET.

O EF Core usa o modelo **Code First**, esse modelo é usado para definir o esquema do banco de dados a partir do código em vez de definir o banco de dados primeiro.
### **1. Criando as entidades**
Criando classes para representar nossas entidades.
![400](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf9_vvkVmaaD1lTbulQoMl2LcmsGY2ygx8fK3xuzeVcsaRvoE9BcL_reZLLb9psjbg-L9IIcj15F4cD2zOd8fi2OaDvDUhOEy46lFZFkcWvPL94FZL3aXwK_azfmaamihVZkfmJp88OTXyWqgUKbhXMLbSN?key=SZHaDLu24DLXyFgiFaRNLA)

![400](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf0hI8Tzva3_fx0hTiYzJamZ0uuEB0SHOxynnXWR7mLyfcvCslWFySwK4W8SLrgEfi9SBIZ0J7Q5Ffzz0rpZ98aX7i6zaHHFe04FaA-uSecCxfaM4o1KdP6BgMUxS5EC-C8_4eDHyRMFQaPK7yof7UlhHSg?key=SZHaDLu24DLXyFgiFaRNLA)

Essas classes são consideradas anêmicas, mas o que é isso? Uma classe é considerada "anêmica" quando não possui lógica de negócio e contém apenas propriedades com métodos getter e setter. Essas classes não têm métodos que encapsulam a lógica de negócio, essa lógica é movida para outro serviço.

---
### **2. Escolhendo o provedor de banco de dados**
Basta adicionar o pacote do banco de dados específico e do EF Core.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfWaQw4UXziG_fURwH6aPv_FipqhqYDTka18htHQKrbvgJ8sfDUlNE99JbG7RIFFwG1R2IDuJYxixGvU-e3YmbnGj_1ORdb0m_0sF9eBL5Yhnz0Y4R2EuIewMhipkvRu4a3EvMNG-sAnzRvTgkjj8NyJiI?key=SZHaDLu24DLXyFgiFaRNLA)![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcdihRD0g69tv2PP2VzaijUqnTwjqKUKf9cix2XEFovPazDO7iuD3XjV8LXLXFpY_QgFq33rtPY9vxszsdYd9aTFfdIqjd8dHZ4uDl3j0twOaWDnghwHZWkOzn8YmDraZgmAHqZbagIqO4uakDA35JSBqNv?key=SZHaDLu24DLXyFgiFaRNLA)

Além de definir as entidades, você define **DbContext** para seu aplicativo. O DbContext é o coração do EF Core em seu aplicativo, e é usado para todas as chamadas ao banco de dados.  
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdJp0dZi6blaAYblVjWW8eZah71bEQzEQ6n6EYtZfeYC1crbEZ9hIoNUTIoNEKQOzg8Is2HQwqh5kBHGv4yghi08tmJvbBA0prAZck33Xmills-L3hWxbR_2y4HDfXN5JTzg2HOwA3wrSi5kviByIfWtM0M?key=SZHaDLu24DLXyFgiFaRNLA)
1️⃣ AppDbContext deriva da classe base DbContext. Esta classe expõe **DbSet<>** para que o EF Core possa descobrir e mapear as entidades.  
2️⃣ options do construtor contém configurações, como a string de conexão.

---
### **2. Registrando um contexto de dados**
Você deve registrar seu AppDbContext no contêiner de DI. Ao registrar seu contexto, você também configura o provedor de banco de dados e a string de conexão.

O EF Core fornece o método de extensão **AddDbContext<>**, o método aceita uma função de configuração para uma instância de **DbContextOptionsBuilder**.![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfeRFle4vLIAlwGwatcCiCukNn9BfyMVimoFKH50apK1jY6NbVaoTZekMXydfFsA0d029SOpTLoWqSJbsC9QDTUDaRMSrs5_B3LbE3Pq1em1tMRQIL6bqiwfeX4Ac5XnK9ksUpLBnPwbmrWwTNmny4w47Fz?key=SZHaDLu24DLXyFgiFaRNLA)
1️⃣  A string de conexão é obtida da configuração, da seção ConnectionStrings. 
2️⃣ Registra o DbContext do seu aplicativo usando-o como parâmetro genérico. 
3️⃣ Especifica o provedor de database nas opções para o DbContext.

A string de conexão é um segredo, então carregá-la da configuração faz sentido. Em tempo de execução, a string correta para o seu ambiente é usada.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdeP1vYWf4ct8ceR_oMTZwmJvehIM9LfIVWmevU3ODPmym70BNpjM4P47vyCO9oUjzW27iLdgQm_SPXRWWmGyNgn6xBWcivLy3bax_2f4C8HLTQW8ns_lWpstYiwvhkfNaV11XypSZuuUPzDaglMlL7Axjf?key=SZHaDLu24DLXyFgiFaRNLA)
