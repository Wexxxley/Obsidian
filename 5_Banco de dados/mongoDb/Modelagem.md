
1. **`users`**:
    - Armazena os documentos de usuário.
    - `UserAddress`: continua **incorporado** dentro do documento `User` (1:1).
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

2. **`products`**:    
    - Contém os documentos de produto principal.
    - Cada documento de produto agora terá apenas os atributos gerais do produto, e **não mais as variações incorporadas**.
    ```json
    {
      "_id": ObjectId("product_id_1"),
      "name": "Camiseta Personalizada",
      "description": "Camiseta de algodão personalizável.",
      "base_price": 49.90,
      "category": "Vestuário"
    }
    ```
    
3. **`product_variations`**:
    - **NOVA COLEÇÃO!** Esta coleção armazenará as variações de produtos.
    - Cada documento de variação terá uma **referência (`product_id`)** para o produto principal.
    - **Relacionamento:** `Product` 1:N `ProductVariation` agora é por **referência**.
    
    ```json
    {
      "_id": ObjectId("variation_id_1"),
      "product_id": ObjectId("product_id_1"), // Referência ao Product
      "sku": "TSHIRT-RED-M",
      "attributes": {"color": "red", "size": "M"},
      "additional_price": 0.00,
      "stock": 100,
      "image_urls": ["url_red_m_1.jpg", "url_red_m_2.jpg"]
    }
    ```

4. **`orders`**:    
    - Guarda os documentos de pedido.
    - Os itens de cada pedido (`items`) continuam **incorporados** como um array dentro do documento de pedido (1:N), pois são intrínsecos ao pedido.
    - Cada pedido também terá uma referência (`user_id`) para o usuário que fez a compra (1:N).
    ```json
    {
      "_id": ObjectId("order_id_1"),
      "user_id": ObjectId("user_id_1"), // Referência ao User
      "order_date": ISODate("2023-07-15T14:30:00Z"),
      "total_amount": 104.90,
      "status": "Pending", // Usar um Enum no código da aplicação
      "payment_method": "Credit Card",
      "items": [
        {
          "product_id": ObjectId("product_id_1"),
          "product_name": "Camiseta Personalizada",
          "selected_sku": "TSHIRT-RED-M",
          "selected_attributes": {"color": "red", "size": "M"},
          "quantity": 1,
          "unit_price": 49.90
        },
        // ... outros OrderItems
      ]
    }
    ```
    
5. **`promotions`**:
    - Armazena os documentos de promoção.
    - Contém um array de IDs de produtos (`applicable_products`) para os quais a promoção se aplica (N:N).
    ```json
    {
      "_id": ObjectId("promotion_id_1"),
      "name": "Black Friday",
      "start_date": ISODate("2023-11-20T00:00:00Z"),
      "end_date": ISODate("2023-11-30T23:59:59Z"),
      "discount_type": "percentage", // Usar Enum
      "discount_value": 0.20, // 20%
      "applicable_products": [
        ObjectId("product_id_1"),
        ObjectId("product_id_2")
      ]
    }
    ```