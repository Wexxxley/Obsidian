
---
### **Definição de Enums** 

- **ItemType:** Define se o registro é um PRODUTO (sujeito a controle de estoque) ou SERVIÇO (sem controle de estoque).
    
- **UnitType:** Determina a unidade de medida do item (UNIDADE, KG, LITRO, METRO).
    
- **CategoryType:** Diferencia se a categoria pertence a ITENS de catálogo ou a DESPESAS operacionais.
    
- **SaleStatus:** Representa o ciclo de vida da venda (ORÇAMENTO, PENDENTE, ATRASADA, FINALIZADA, CANCELADA).
    
- **InstallmentStatus:** Indica o estado de cada parcela individual (PENDENTE, PAGA, ATRASADA).
    
- **PaymentMethod:** Lista os meios de recebimento (DINHEIRO, PIX, DÉBITO, CRÉDITO, FIADO).

### 1. Infraestrutura e Configuração Base

- [ ] Configurar as dependências do Room e KSP no arquivo `build.gradle` do módulo.
    
- [ ] Criar a classe `TypeConverters` para gerenciar a conversão de `UUID`, `Date/Long` e dos Enums definidos acima para formatos compatíveis com o SQLite.
    
- [ ] Implementar a classe abstrata `AppDatabase` configurando a versão inicial e os `TypeConverters`.
    
- [ ] Estabelecer o padrão de injeção de dependência para prover a instância única do banco de dados para a camada de serviços.
    

### 2. Modelagem das Entidades (Schema)

- [ ] Criar `CategoryEntity`: Incluir `id` (UUID), `nome` e `tipo` (CategoryType).
    
- [ ] Criar `ProductEntity`: Incluir `id` (UUID), `categoryId` (opcional), `nome`, `precoCusto`, `precoVenda`, `unidadeMedida`, `tipoItem`, `quantidadeEstoque` (Double) e `imagePath` (String para o caminho do arquivo).
    
- [ ] Criar `ClientEntity`: Incluir `id` (UUID), `nome`, `telefone` (apenas números), `endereco` e `imagePath`.
    
- [ ] Criar `SaleEntity`: Incluir `id` (UUID), `clientId` (obrigatório para vendas a prazo), `dataVenda`, `status` e `valorTotal`.
    
- [ ] Criar `SaleItemEntity`: Incluir `id` (UUID), `saleId`, `productId` (null para itens avulsos), `nomeCustomizado`, `quantidade`, `custoUnitarioNoAto` e `precoVendaNoAto`.
    
- [ ] Criar `InstallmentEntity`: Incluir `id` (UUID), `saleId`, `numeroParcela`, `valor`, `dataVencimento`, `dataPagamento` (nullable) e `statusParcela`.
    

### 3. Implementação dos DAOs e Queries de Negócio

- [ ] Implementar `CategoryDao` com suporte a filtros por `CategoryType`.
    
- [ ] Implementar `ClientDao` com busca otimizada por nome e filtragem de caracteres não numéricos no telefone.
    
- [ ] Implementar `ProductDao` contendo a query específica para atualização atômica de saldo e custo médio.
    
- [ ] Criar `InstallmentDao` com as seguintes funções críticas:
    
    - [ ] Consulta de todas as parcelas pendentes ou atrasadas de um cliente específico via `JOIN` com `SaleEntity`.
        
    - [ ] Soma do débito total por cliente (Agregação).
        
- [ ] Implementar `SaleDao` com o relacionamento `@Relation` para retornar a venda completa acompanhada de todos os seus itens e parcelas (`SaleWithDetails`).
    

### 4. Lógica de Serviços e Casos de Borda (Core Backend)

- [ ] Implementar o serviço de Produto: Garantir que serviços tenham estoque bloqueado em zero e que o `imagePath` seja validado antes da persistência.
    
- [ ] Implementar o cálculo de Custo Médio Ponderado: Aplicar a fórmula matemática ao registrar entradas de estoque e persistir o novo valor no produto.
    
- [ ] Implementar o gerador de parcelas:
    
    - [ ] Dividir o valor total da venda pelo número de parcelas.
        
    - [ ] Realizar o ajuste de centavos (arredondamento) na última parcela.
        
    - [ ] Calcular as datas de vencimento sucessivas.
        
- [ ] Implementar a lógica de baixa de pagamentos:
    
    - [ ] Registrar o recebimento de uma `InstallmentEntity`.
        
    - [ ] Verificar se todas as parcelas da venda vinculada foram pagas.
        
    - [ ] Em caso positivo, atualizar automaticamente o status da `SaleEntity` para FINALIZADA.
        

### 5. Validação e Testes de Integridade

- [ ] Criar testes unitários para a fórmula de custo médio ponderado, simulando entradas sucessivas de mercadorias.
    
- [ ] Desenvolver testes de persistência para garantir que nenhum ID incremental seja utilizado, validando o uso estrito de UUIDs.
    
- [ ] Testar o cenário de pagamento parcial: Validar se a venda permanece em status PENDENTE enquanto houver ao menos uma parcela não paga.
    
- [ ] Validar a exclusão em cascata: Garantir que, ao cancelar ou excluir uma venda, os itens e parcelas relacionados sejam tratados conforme a regra de negócio (estorno ou exclusão).
    

O cálculo do custo médio ponderado é fundamental para a saúde financeira do negócio, pois determina o lucro real em cada venda. Para auxiliar na compreensão da lógica que será implementada no backend, o simulador abaixo permite observar como o custo unitário se comporta com diferentes volumes e preços de compra.

Este recurso visual ajudou você a entender melhor a resposta?

SimNão