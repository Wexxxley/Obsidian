
---
É **possível ter relacionamentos no MongoDB**, mas a forma como eles são implementados e a frequência com que são utilizados diferem significativamente dos bancos de dados relacionais.

No MongoDB, os relacionamentos são geralmente gerenciados de duas formas principais:

1. **Modelagem por Incorporação (Desnormalização):**
    - Nesse modelo, você incorpora um documento dentro de outro. Ou seja, você armazena os dados relacionados diretamente dentro do documento principal.
    - **Exemplo:** Em vez de ter uma coleção separada para "endereços", os endereços são incorporados diretamente no documento do "usuário".
    - **Quando usar:** É a abordagem preferencial no MongoDB para dados que são frequentemente acessados juntos, que são pequenos, ou que não mudam independentemente do documento principal.
    - **Desvantagens:** Pode levar à duplicação de dados se o mesmo dado incorporado precisar aparecer em múltiplos documentos.
	```json
	{
	  "_id": ObjectId("..."),
	  "name": "João Silva",
	  "email": "joao.silva@example.com",
	  "registration_date": ISODate("2023-01-15T10:00:00Z"),
	  "phone_number": "5511987654321",
	  "shipping_address": {
	    "street": "Rua das Flores",
	    "number": "123",
	    "complement": "Apt 101",
	    "neighborhood": "Centro",
	    "city": "São Paulo",
	    "state": "SP",
	    "cep": "01000-000"
	  }
	}
	```


```json
    {
      "_id": ObjectId("..."),
      "name": "Camiseta Personalizada",
      "description": "Camiseta de algodão personalizável.",
      "base_price": 49.90,
      "category": "Vestuário", // Usar um Enum no código da aplicação
      "variations": [
        {
          "sku": "TSHIRT-RED-M",
          "attributes": {"color": "red", "size": "M"},
          "additional_price": 0.00,
          "stock": 100,
          "image_urls": ["url_red_m_1.jpg", "url_red_m_2.jpg"]
        },
        {
          "sku": "TSHIRT-BLUE-L",
          "attributes": {"color": "blue", "size": "L"},
          "additional_price": 5.00,
          "stock": 50,
          "image_urls": ["url_blue_l_1.jpg"]
        }
      ]
    }
    ```

2. **Modelagem por Referência (Normalização):**
    - Nesse modelo, você armazena o `_id` de um documento em outro documento, criando uma "referência". É o equivalente a usar chaves estrangeiras em um banco de dados relacional.
    - **Quando usar:** É a melhor abordagem quando os dados relacionados são grandes, mudam com frequência, ou quando você precisa consultar os dados separadamente. 
    - **Consultas:** Para obter os dados completos, você precisará fazer duas consultas: uma para o livro e outra para o autor. O MongoDB possui operadores como `$lookup` (similar a um `JOIN` em SQL) para facilitar isso, mas é importante entender que ele funciona de forma diferente e pode ter implicações de performance em grandes volumes de dados.

```json

{
  "_id": ObjectId("..."),
  "name": "Black Friday",
  "start_date": ISODate("2023-11-20T00:00:00Z"),
  "end_date": ISODate("2023-11-30T23:59:59Z"),
  "discount_type": "percentage", // Usar Enum
  "discount_value": 0.20, // 20%
  "applicable_products": [
    ObjectId("product_id_1"),
    ObjectId("product_id_2"),
    ObjectId("product_id_3")
  ]
}
```