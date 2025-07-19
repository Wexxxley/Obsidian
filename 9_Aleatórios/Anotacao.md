
### **1. Recuperar Histórico de Pedidos Completo de um Usuário Específico:**

- **Objetivo:** Obter todos os pedidos de um usuário, com os detalhes completos de cada produto comprado (incluindo nome, preço atual, marca, e detalhes da variação selecionada no momento da compra).
    
- **Coleções Envolvidas:** `UserBaseModel`, `PedidoBaseModel`, `ItemPedido`, `ProdutoBaseModel`, `VariacaoBaseModel`.
    
- **Lógica:**
    
    1. Encontrar o `_id` do usuário.
        
    2. `$lookup` na coleção `PedidoBaseModel` usando `id_usuario`.
        
    3. `$unwind` nos `items` de cada `PedidoBaseModel` para processar cada item individualmente.
        
    4. `$lookup` em `ProdutoBaseModel` usando `id_produto` de `ItemPedido`.
        
    5. `$lookup` em `VariacaoBaseModel` usando `id_produto` e `sku_selecionado` (se o SKU for único globalmente ou dentro do produto) para pegar detalhes da variação.
        
    6. Reconstruir a estrutura do pedido com todos os detalhes.
        
- **Perguntas que responde:** Qual o histórico de compras de um cliente? Quais produtos específicos (com variações) ele comprou? Quanto ele gastou em cada pedido?
### **6. Produtos Atualmente em Promoção e Detalhes da Promoção:**

- **Objetivo:** Gerar uma lista de produtos em promoção com seus detalhes de preço original e preço promocional.
    
- **Coleções Envolvidas:** `ProdutoBaseModel`, `PromocaoBaseModel`, `VariacaoBaseModel`.
    
- **Lógica:**
    
    1. Começar com `PromocaoBaseModel` e `$match` para promoções ativas (`data_inicio` <= hoje e `data_fim` >= hoje).
        
    2. `$unwind` em `produtos_aplicaveis`.
        
    3. `$lookup` em `ProdutoBaseModel` usando `id_produto` (de `produtos_aplicaveis`).
        
    4. `$lookup` em `VariacaoBaseModel` para pegar detalhes das variações desse produto (assumindo que a promoção se aplica a todas as variações ou a lógica de aplicação será mais complexa).
        
    5. Calcular o preço com desconto com base no `tipo_desconto` e `valor_desconto`.
        
- **Perguntas que responde:** Quais produtos estão em promoção agora? Qual o desconto oferecido e o preço final?