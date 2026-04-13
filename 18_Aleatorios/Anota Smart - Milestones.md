
#Concluded 

---
## **1. Backend**
### Definição de Enums

Os enums representam o domínio do sistema e serão salvos no banco de dados.
- **ItemType:** PRODUTO ou SERVIÇO.
- **UnitType:** UNIDADE, KG, LITRO, METRO.
- **CategoryType:** ITENS ou DESPESAS.
- **SaleStatus:** ORÇAMENTO, PENDENTE, ATRASADA, FINALIZADA, CANCELADA.
- **InstallmentStatus:** PENDENTE, PAGA, ATRASADA.
- **PaymentMethod:** DINHEIRO, PIX, DÉBITO, CRÉDITO.

### 1. Infraestrutura e Configuração Base

- [ ] Configurar exclusivamente as dependências essenciais do Room (Runtime, KTX) e KSP no arquivo `build.gradle` do módulo.
    
- [ ] Criar a classe `TypeConverters` restrita apenas à conversão dos Enums para `String` (e vice-versa), utilizando a propriedade `.name` nativa do Kotlin.
    
- [ ] Implementar a classe abstrata `AppDatabase` configurando a versão inicial e registrando o `TypeConverters` dos Enums.
    
- [ ] Implementar a instanciação manual do banco de dados (Singleton) utilizando uma classe base que herda de `Application` no Android, provendo o `AppDatabase` globalmente sem frameworks externos de injeção de dependência.    

### 2. Modelagem das Entidades 

ids serao uuid mas o tipo nativo utilizado será `String`

Table Category {
id varchar [primary key]
nome varchar
tipo CategoryType
}

Table Product {
id varchar [primary key]
categoryId varchar [null]
nome varchar
precoCusto double
precoVenda double
unidadeMedida UnitType
tipoItem ItemType
quantidadeEstoque double
imagePath varchar
}


Table Client {
id varchar [primary key]
nome varchar
telefone varchar [note: 'Apenas números']
endereco text
imagePath varchar
}

Table Sale {
id varchar [primary key]
clientId varchar [null, note: 'Permite venda avulsa sem cliente']
dataVenda long [note: 'Milissegundos']
status SaleStatus
valorTotal double
}

Table SaleItem {
id varchar [primary key]
saleId varchar
productId varchar [null, note: 'Permite adicionar itens que não estão no catálogo']
nomeCustomizado varchar
quantidade double
custoUnitarioNoAto double
precoVendaNoAto double
}

Table Installment {
id varchar [primary key]
saleId varchar
numeroParcela integer
valor double
dataVencimento long
dataPagamento long [null]
statusParcela InstallmentStatus
metodoPagamento PaymentMethod [null, note: 'Preenchido apenas quando a parcela é paga']

}

// --- Definição das Ligações (Relacionamentos) ---
// Um produto pode ter uma categoria
Ref: Product.categoryId > Category.id
// Uma venda pode opcionalmente estar ligada a um cliente
Ref: Sale.clientId > Client.id
// Itens de venda pertencem a uma vend
Ref: SaleItem.saleId > Sale.id
// Um item de venda pode referenciar um produto (opcional para itens avulsos)
Ref: SaleItem.productId > Product.id
Ref: Installment.saleId > Sale.id

![](../attachments/Pasted%20image%2020260412173414.png)

**1. Ocorrência de Venda Fiada (A Prazo):** No momento em que a venda é registrada como fiado, o sistema gera as instâncias de `InstallmentEntity`. Nesse momento, o `statusParcela` é definido como `PENDENTE`, a `dataPagamento` é nula e o `metodoPagamento` também é nulo. A dívida existe formalmente no sistema, mas a liquidação ainda não ocorreu.

**2. Ocorrência da Liquidação (Baixa da Dívida):** Quando o cliente retorna ao estabelecimento para quitar a parcela pendente, o sistema deve registrar esse evento. A aplicação atualizará o registro específico da `InstallmentEntity`: o `statusParcela` é alterado para `PAGA`, a `dataPagamento` recebe o timestamp atual (`Long`), e o `metodoPagamento` é finalmente preenchido com a forma escolhida pelo cliente naquele momento (por exemplo, `PIX` ou `DINHEIRO`).

**3. Ocorrência de Venda à Vista:** Para unificar a arquitetura e evitar lógicas duplicadas, toda venda à vista também deve gerar uma `InstallmentEntity`. A diferença é que o sistema pulará a etapa de pendência. A parcela é criada imediatamente com `statusParcela` igual a `PAGA`, a `dataPagamento` com o timestamp atual e o `metodoPagamento` já preenchido com a forma utilizada no balcão.

---
### 3. DAOs

CategoryDao

Responsável pelo gerenciamento das categorias do catálogo e das despesas. Como o volume de categorias costuma ser pequeno, não há necessidade de paginação.

- `insert(category: Category)`    
- `update(category: Category)`
- `delete(category: Category)`
- `getByType(type: String): List<Category>`: Filtra especificamente para separar categorias de itens das categorias de despesas operacionais.

ClientDao

Gerencia a base de clientes do aplicativo, otimizada para listagens e buscas rápidas. A listagem geral recebe paginação para não sobrecarregar a memória do dispositivo
- `insert(client: Client)`
- `update(client: Client)`
- `getById(id: String): Client?`: Carrega o perfil completo para a tela de edição.
- `getAllOrderedByNamePaginated(limit: Int, offset: Int): List<Client>`: Retorna a lista completa ordenada alfabeticamente. Utiliza paginação (`LIMIT :limit OFFSET :offset`) para carregar a lista sob demanda (lazy loading).
- `searchByName(query: String): List<Client>`: Utiliza a cláusula SQL `LIKE` para filtrar clientes em tempo real durante a digitação na barra de pesquisa.
    

ProductDao

Centraliza o acesso aos itens do catálogo e a lógica crítica de atualização de estoque financeiro. O catálogo tende a crescer, portanto as listagens principais são paginadas.

- `insert(product: Product)`
    
- `update(product: Product)`: Executa a atualização completa do registro (utilizada ao editar nome, categoria ou foto).
    
- `getById(id: String): Product?`
    
- `getAllPaginated(limit: Int, offset: Int): List<Product>`: Retorna os produtos utilizando paginação (`LIMIT :limit OFFSET :offset`) para a tela principal de catálogo.
    
- `getByCategoryIdPaginated(categoryId: String, limit: Int, offset: Int): List<Product>`: Retorna produtos filtrados por categoria, também sob demanda via `LIMIT` e `OFFSET`.
    
- `updateStockAndCost(id: String, newStock: Double, newCost: Double)`: Utiliza a anotação `@Query` para executar uma instrução SQL nativa que atualiza apenas o saldo e o custo médio de forma atômica e segura, sem carregar o objeto inteiro na memória.
    

SaleItemDao

Gerencia os registros individuais dos itens vinculados a uma venda específica. Como o número de itens por venda é naturalmente limitado pelo contexto físico, não requer paginação.

- `insertAll(items: List<SaleItem>)`: Persiste todos os itens do carrinho de compras em uma única transação no banco de dados.
    
- `getBySaleId(saleId: String): List<SaleItem>`: Busca a lista de itens pertencentes a uma venda, essencial para carregar os detalhes do recibo.
    

InstallmentDao

Concentra a lógica financeira complexa, cruzando dados de parcelas e vendas para determinar inadimplência e quitação. As consultas retornam volumes controlados (apenas o que está pendente para um cliente específico), dispensando paginação.

- `insertAll(installments: List<Installment>)`: Salva o cronograma completo de pagamentos gerado no momento de uma venda a prazo.
    
- `updatePayment(id: String, paymentDate: Long, method: String, status: String)`: Query nativa de atualização que executa a baixa da parcela, preenchendo os dados de liquidação.
    
- `getPendingByClientId(clientId: String): List<Installment>`: Requer a utilização de um `INNER JOIN` com a tabela `Sale` para filtrar e retornar apenas as parcelas cujo status seja diferente de paga, pertencentes àquele cliente.
    
- `getTotalDebtByClientId(clientId: String): Double`: Utiliza a função de agregação `SUM(amount)` do SQLite para calcular e retornar o valor total devido pelo cliente com base nas parcelas não pagas.
    
- `countPendingBySaleId(saleId: String): Int`: Utiliza a função `COUNT` para verificar quantas parcelas abertas restam para uma venda específica. Atua como o gatilho de verificação para a Controller alterar o status da Venda matriz para finalizada.
    

SaleDao

Gerencia o ciclo de vida da venda principal e as consultas relativas ao fluxo de caixa do negócio. O histórico de vendas é potencialmente infinito, exigindo paginação.

- `insert(sale: Sale)`
    
- `updateStatus(saleId: String, newStatus: String)`: Query SQL nativa para alterar rapidamente o status sem necessidade de instanciar a entidade completa.
    
- `getSalesHistoryPaginated(limit: Int, offset: Int): List<Sale>`: Consulta adicionada para listar as vendas passadas de forma cronológica decrescente, utilizando `LIMIT :limit OFFSET :offset` para renderização em blocos.
    
- `getSaleWithDetails(saleId: String): SaleWithDetails`: Retorna uma classe de dados que utiliza a anotação `@Relation` do Room para agrupar a instância de `Sale` com suas respectivas listas filhas de `SaleItem` e `Installment`.
    
- `getProfitabilityReport(startDate: Long, endDate: Long): List<Sale>`: Consulta vital para o módulo financeiro. Utiliza a cláusula SQL `BETWEEN` nos campos de data (`Long`) para filtrar o período, aplicando obrigatoriamente a restrição de que o status seja igual a 'FINALIZADA'. Esta consulta não é paginada pois o relatório precisa de todos os registros do período de uma só vez para os cálculos de totalização.

---
### 4. CategoryViewModel

- [ ] Implementar a `CategoryViewModel`:
    - Criar `StateFlow` para expor a lista de categorias para a UI.
    - `loadCategories(type: CategoryType)` acessando o DAO. 
    - `saveCategory(idAtual: String?, nome: String, tipo: CategoryType)`: Se `idAtual` for nulo, gera o UUID e insere; caso contrário, atualizar. Deve aplicar `.trim()` no nome e verificar se está vazio (`isBlank()`). Se estiver, deve abortar a operação e emitir um erro para a UI ("Categoria não pode estar vazia").
    - Implementar função `deleteCategory(category: Category)`.

Bloco A: Testes de Validação e Limites (Failing Fast)
- [ ] **Teste de Validação de Nome Vazio:** Chamar `saveCategory` passando `nome = ""` e ID nulo.
    - _Assertividade:_ Garantir que a função retorne um erro e que o método `insert` do DAO nunca seja chamado
- [ ] **Teste de Validação de Nome Apenas com Espaços:** Chamar `saveCategory` passando `nome = " "`.
    - _Assertividade:_ Garantir que a ViewModel aplique o `trim()` e trate como vazio, bloqueando a ida ao DAO.
- [ ] **Teste de ID "Falso Nulo":** Chamar `saveCategory` passando `idAtual = ""` (String vazia) em vez de `null`.
    - _Assertividade:_ Garantir que a ViewModel seja inteligente o suficiente para identificar que String vazia significa "Novo Cadastro", gerando um UUID válido e chamando o `insert` (e não o `update`).

Bloco B: Testes de Persistência (Happy Path)
- [ ] **Teste de Inserção de Nova Categoria:** Chamar `saveCategory` com ID nulo, nome "Ferramentas" e tipo `ITEM`.    
    - _Assertividade:_ Garantir que o DAO receba o objeto exato chamado via `insert`, com um ID que seja um UUID válido de 36 caracteres, e que o estado mude para `Success`.
- [ ] **Teste de Atualização de Categoria Existente:** Chamar `saveCategory` com ID "123-abc", nome "Ferramentas Manuais" e tipo `ITEM`.
    - _Assertividade:_ Garantir que o método `update` do DAO seja chamado preservando estritamente o ID "123-abc", e que o `insert` nunca seja chamado.
        
- [ ] **Teste de Exclusão Física:** Chamar `deleteCategory` passando uma categoria válida.
    - _Assertividade:_ Verificar se o método `delete` do DAO foi chamado com o mesmo objeto e se a lista na memória foi recarregada para refletir a exclusão.

#### Bloco C: Testes de Busca e Estado (Data Retrieval)
- [ ] **Teste de Carregamento Filtrado:** Chamar `loadCategories(CategoryType.EXPENSE)`.
    - _Configuração:_ Mockar o DAO para retornar 2 categorias de despesas.
    - _Assertividade:_ Garantir que o `StateFlow` emita `Loading` e logo após emita `Success` contendo exatamente a lista com os 2 itens retornados pelo DAO.
        
- [ ] **Teste de Lista Vazia:** Chamar `loadCategories` quando o banco não tem categorias registradas.
    - _Assertividade:_ O `StateFlow` deve emitir `Success` com uma lista vazia `[]`, garantindo que a tela não quebre ao tentar renderizar o vazio.
        


---

### 3. Módulo de Clientes (`ClientViewModel`)

- [ ] Implementar a `ClientViewModel`:
    
    - Configurar estado de paginação (`currentPage`, `PAGE_SIZE = 20`, `isLoading`, `isLastPage`).
        
    - Criar `StateFlow` para expor a lista unificada de clientes.
        
    - Implementar `loadMoreClients()` calculando o `offset` e concatenando os resultados do DAO à lista em memória.
        
    - Implementar `searchClients(query: String)`: Limpar a lista atual, resetar paginação e chamar busca por nome.
        
    - Implementar função de Upsert `saveClient(idAtual, nome, telefone, endereco, imagePath)`: Aplicar um `.filter { it.isDigit() }` no telefone antes de enviar ao DAO.
        
- [ ] Criar testes para `ClientViewModelTest`:
    
    - Teste 1: Validar a lógica de paginação (simular rolagem e garantir que o offset é calculado corretamente como 0, 20, 40...).
        
    - Teste 2: Validar a higienização do telefone (garantir que "(88) 99999-1234" seja convertido e salvo estritamente como "88999991234").
        

---

### 4. Módulo de Produtos e Estoque (`ProductViewModel`)

- [ ] Implementar a `ProductViewModel`:
    
    - Configurar paginação (`loadMoreProducts`) análoga à de clientes.
        
    - Implementar função de Upsert `saveProduct(idAtual, categoryId, nome, custo, venda, unidade, tipoItem, imagePath)`:
        
        - **Regra de Negócio:** Se `tipoItem == ItemType.SERVICE`, forçar a propriedade `quantidadeEstoque = 0.0`.
            
    - Implementar função financeira `registerStockEntry(productId, qtdNova, precoNovo)`:
        
        - Buscar dados atuais do produto via DAO.
            
        - Calcular o Custo Médio Ponderado: `((qtdAtual * custoAtual) + (qtdNova * precoNovo)) / (qtdAtual + qtdNova)`.
            
        - Chamar `productDao.updateStockAndCost` com os novos valores.
            
- [ ] Criar testes para `ProductViewModelTest`:
    
    - Teste 1: Garantir que tentar cadastrar ou editar um item do tipo `SERVICE` resulte sempre em um objeto com estoque zero, independente do valor digitado na UI.
        
    - Teste 2: Validar a matemática do CMP com uma entrada válida (ex: 10 itens a R$50 + 5 itens a R$65 devem resultar em um novo custo médio exato de R$55.00).
        
    - Teste 3: Validar a prevenção de erro matemático do CMP: garantir que, se o novo saldo de estoque for zero, o custo médio assuma 0.0 (evita `ArithmeticException` por divisão por zero).
        

---

### 5. Módulo de Vendas e PDV (`SaleViewModel`)

- [ ] Implementar a `SaleViewModel`:
    
    - Criar `StateFlow` gerenciando o Carrinho de Compras (`List<SaleItem>`) e o Total Dinâmico da Venda.
        
    - Implementar funções de carrinho: `addItem`, `removeItem`, `updateQuantity`.
        
    - Implementar função crítica `checkout(clientId, parcelas, prazoEmDias)`:
        
        - Gerar UUID da Venda Mestre e salvar no `SaleDao` com status `PENDING`.
            
        - Iterar o carrinho, gerar UUID para cada `SaleItem` vinculando ao ID da Venda e salvar no `SaleItemDao`.
            
        - **Gerador de Parcelas:** - Dividir o total pelo número de parcelas (truncando para 2 casas decimais).
            
            - Calcular a diferença (centavos) para a última parcela (`total - (valorBase * (parcelas - 1))`).
                
            - Gerar as instâncias de `Installment`, calculando as datas de vencimento sequenciais (`System.currentTimeMillis() + (i * prazoEmDias * 86400000L)`).
                
            - Salvar lista no `InstallmentDao`.
                
        - Limpar o carrinho após sucesso.
            
- [ ] Criar testes para `SaleViewModelTest`:
    
    - Teste 1: Validar o arredondamento financeiro da geração de parcelas (ex: Venda de R$ 100.00 em 3x deve gerar parcelas de 33.33, 33.33 e 33.34. A soma absoluta deve ser igual a 100.00).
        
    - Teste 2: Validar o carrinho de compras: garantir que tentar fazer `checkout` com o carrinho vazio emita um erro ou exceção mapeada.
        
    - Teste 3: Validar o cálculo de datas de vencimento: certificar que a primeira parcela de uma venda em 30 dias tenha o `dueDate` exatamente 30 dias (em milissegundos) à frente do timestamp atual.
        

---

### 6. Módulo Financeiro e Baixas (`ReceivableViewModel`)

- [ ] Implementar a `ReceivableViewModel`:
    
    - Implementar função `loadPendingByClient(clientId)` para popular a tela de cobrança de um cliente.
        
    - Implementar função `loadTotalDebt(clientId)` para exibir o consolidado do cliente.
        
    - Implementar função crítica de gatilho `receivePayment(installmentId, saleId, method)`:
        
        - Registrar a data de hoje no formato Long.
            
        - Chamar `installmentDao.updatePayment` passando `InstallmentStatus.PAGA.name` e o `method.name`.
            
        - Chamar `installmentDao.countPendingBySaleId(saleId)`.
            
        - **Gatilho de Finalização:** Se a contagem retornar 0, chamar `saleDao.updateStatus(saleId, SaleStatus.FINISHED.name)`.
            
- [ ] Criar testes para `ReceivableViewModelTest`:
    
    - Teste 1: Simular o pagamento da parcela 1 de 2. Afirmar que o DAO de `Installment` foi chamado, mas o DAO de `Sale` (para finalizar a venda) NÃO foi chamado.
        
    - Teste 2: Simular o pagamento da última parcela pendente de uma venda. Afirmar que a verificação de contagem foi executada e que o `saleDao.updateStatus` foi invocado com o status `FINISHED`.


### 1. Camada de Infraestrutura e Injeção Manual

Como não usaremos bibliotecas como Hilt ou Koin, precisamos das fábricas nativas para instanciar as ViewModels passando os DAOs.

- [ ] Implementar a `ViewModelFactory` mestre ou fábricas individuais:
    
    - Criar classe que herda de `ViewModelProvider.Factory`.
        
    - Sobrescrever o método `create` para instanciar `CategoryViewModel`, `ClientViewModel`, `ProductViewModel`, `SaleViewModel` e `ReceivableViewModel`, injetando os respectivos DAOs vindos da instância Singleton do `AppDatabase`.
        