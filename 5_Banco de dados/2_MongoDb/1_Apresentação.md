
---
O MongoDB é um sistema de banco de dados NoSQL, o que significa que ele se difere bastante dos bancos de dados relacionais tradicionais.

Em vez de tabelas, linhas e colunas, o MongoDB usa uma estrutura baseada em **documentos** e **coleções**.

![500](attachments/Pasted%20image%2020250717141001.png)
### **1. Documentos**
A unidade de dados no MongoDB é o **documento BSON** (Binary JSON). Um documento pode conter campos, arrays e até mesmo outros documentos aninhados. Essa flexibilidade permite representar dados complexos de forma natural.
```json
{
  "_id": ObjectId("60c72b2f9c3c4e001f8e4a9e"),
  "nome": "João Silva",
  "idade": 30,
  "email": "joao.silva@example.com",
  "enderecos": [
	{
	  "rua": "Rua das Flores",
	  "numero": "123",
	  "cidade": "São Paulo"
	},
	{
	  "rua": "Av. Principal",
	  "numero": "456",
	  "cidade": "Rio de Janeiro"
	}
  ],
  "status": "ativo"
}
        ```
- Note o campo `_id`é um identificador único gerado automaticamente pelo MongoDB.
![400](attachments/Pasted%20image%2020250717140911.png)
### **2. Coleções**
Uma **coleção** é um grupo de documentos. É o equivalente a uma "tabela". Mas ao contrário de uma tabela, os documentos dentro de uma coleção não precisam ter a mesma estrutura, o que confere ao MongoDB sua característica de **esquema flexível**. No entanto, na prática, é comum que os documentos dentro de uma coleção tenham estruturas semelhantes.

### **3. Bancos de Dados**
Um **banco de dados** no MongoDB é um contêiner para coleções. Você pode ter múltiplos bancos de dados em uma única instância do MongoDB.
