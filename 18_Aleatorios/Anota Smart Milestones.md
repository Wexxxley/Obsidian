Estratégia "vanilla" consiste em remover bibliotecas de terceiros (como frameworks de Injeção de Dependência, ex: Hilt ou Koin) e reduzir a complexidade interna do Room.

Para isso, os identificadores únicos serão tratados nativamente como `String` no banco de dados (gerados via `java.util.UUID.randomUUID().toString()`), e as datas serão salvas diretamente como `Long` (timestamps). Isso elimina a necessidade de criar conversores complexos, mantendo o banco de dados leve. Além disso, a arquitetura dispensará a camada de Serviço, executando as regras diretamente nos Controllers ou ViewModels.
### Definição de Enums

Os enums representam o domínio do sistema e serão salvos no banco de dados.
- **ItemType:** PRODUTO ou SERVIÇO.
- **UnitType:** UNIDADE, KG, LITRO, METRO.
- **CategoryType:** ITENS ou DESPESAS.
- **SaleStatus:** ORÇAMENTO, PENDENTE, ATRASADA, FINALIZADA, CANCELADA.
- **InstallmentStatus:** PENDENTE, PAGA, ATRASADA.
- **PaymentMethod:** DINHEIRO, PIX, DÉBITO, CRÉDITO.

### 1. Infraestrutura e Configuração Base (Vanilla)

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

### 1. CategoryDao

Responsável pelo gerenciamento das categorias do catálogo e das despesas. Como o volume de categorias costuma ser pequeno, não há necessidade de paginação.

- `insert(category: Category)`
    
- `update(category: Category)`
    
- `delete(category: Category)`
    
- `getByType(type: String): List<Category>`: Filtra especificamente para separar categorias de itens das categorias de despesas operacionais.
    

### 2. ClientDao

Gerencia a base de clientes do aplicativo, otimizada para listagens e buscas rápidas. A listagem geral recebe paginação para não sobrecarregar a memória do dispositivo.

- `insert(client: Client)`
    
- `update(client: Client)`
    
- `getById(id: String): Client?`: Carrega o perfil completo para a tela de edição.
    
- `getAllOrderedByNamePaginated(limit: Int, offset: Int): List<Client>`: Retorna a lista completa ordenada alfabeticamente. Utiliza paginação (`LIMIT :limit OFFSET :offset`) para carregar a lista sob demanda (lazy loading).
    
- `searchByName(query: String): List<Client>`: Utiliza a cláusula SQL `LIKE` para filtrar clientes em tempo real durante a digitação na barra de pesquisa.
    

### 3. ProductDao

Centraliza o acesso aos itens do catálogo e a lógica crítica de atualização de estoque financeiro. O catálogo tende a crescer, portanto as listagens principais são paginadas.

- `insert(product: Product)`
    
- `update(product: Product)`: Executa a atualização completa do registro (utilizada ao editar nome, categoria ou foto).
    
- `getById(id: String): Product?`
    
- `getAllPaginated(limit: Int, offset: Int): List<Product>`: Retorna os produtos utilizando paginação (`LIMIT :limit OFFSET :offset`) para a tela principal de catálogo.
    
- `getByCategoryIdPaginated(categoryId: String, limit: Int, offset: Int): List<Product>`: Retorna produtos filtrados por categoria, também sob demanda via `LIMIT` e `OFFSET`.
    
- `updateStockAndCost(id: String, newStock: Double, newCost: Double)`: Utiliza a anotação `@Query` para executar uma instrução SQL nativa que atualiza apenas o saldo e o custo médio de forma atômica e segura, sem carregar o objeto inteiro na memória.
    

### 4. SaleItemDao

Gerencia os registros individuais dos itens vinculados a uma venda específica. Como o número de itens por venda é naturalmente limitado pelo contexto físico, não requer paginação.

- `insertAll(items: List<SaleItem>)`: Persiste todos os itens do carrinho de compras em uma única transação no banco de dados.
    
- `getBySaleId(saleId: String): List<SaleItem>`: Busca a lista de itens pertencentes a uma venda, essencial para carregar os detalhes do recibo.
    

### 5. InstallmentDao

Concentra a lógica financeira complexa, cruzando dados de parcelas e vendas para determinar inadimplência e quitação. As consultas retornam volumes controlados (apenas o que está pendente para um cliente específico), dispensando paginação.

- `insertAll(installments: List<Installment>)`: Salva o cronograma completo de pagamentos gerado no momento de uma venda a prazo.
    
- `updatePayment(id: String, paymentDate: Long, method: String, status: String)`: Query nativa de atualização que executa a baixa da parcela, preenchendo os dados de liquidação.
    
- `getPendingByClientId(clientId: String): List<Installment>`: Requer a utilização de um `INNER JOIN` com a tabela `Sale` para filtrar e retornar apenas as parcelas cujo status seja diferente de paga, pertencentes àquele cliente.
    
- `getTotalDebtByClientId(clientId: String): Double`: Utiliza a função de agregação `SUM(amount)` do SQLite para calcular e retornar o valor total devido pelo cliente com base nas parcelas não pagas.
    
- `countPendingBySaleId(saleId: String): Int`: Utiliza a função `COUNT` para verificar quantas parcelas abertas restam para uma venda específica. Atua como o gatilho de verificação para a Controller alterar o status da Venda matriz para finalizada.
    

### 6. SaleDao

Gerencia o ciclo de vida da venda principal e as consultas relativas ao fluxo de caixa do negócio. O histórico de vendas é potencialmente infinito, exigindo paginação.

- `insert(sale: Sale)`
    
- `updateStatus(saleId: String, newStatus: String)`: Query SQL nativa para alterar rapidamente o status sem necessidade de instanciar a entidade completa.
    
- `getSalesHistoryPaginated(limit: Int, offset: Int): List<Sale>`: Consulta adicionada para listar as vendas passadas de forma cronológica decrescente, utilizando `LIMIT :limit OFFSET :offset` para renderização em blocos.
    
- `getSaleWithDetails(saleId: String): SaleWithDetails`: Retorna uma classe de dados que utiliza a anotação `@Relation` do Room para agrupar a instância de `Sale` com suas respectivas listas filhas de `SaleItem` e `Installment`.
    
- `getProfitabilityReport(startDate: Long, endDate: Long): List<Sale>`: Consulta vital para o módulo financeiro. Utiliza a cláusula SQL `BETWEEN` nos campos de data (`Long`) para filtrar o período, aplicando obrigatoriamente a restrição de que o status seja igual a 'FINALIZADA'. Esta consulta não é paginada pois o relatório precisa de todos os registros do período de uma só vez para os cálculos de totalização.

### 4. Lógica de Negócios Direta (Controllers / ViewModels)

A execução das regras será feita diretamente na camada de controle (ex: `ProductController` ou `SaleViewModel`), acessando os DAOs de forma direta para manter a simplicidade do fluxo.

- [ ] Implementar a regra de Produto na Controller: Ao salvar, validar imediatamente se o tipo é SERVIÇO para forçar o estoque a 0.0 e gerar o `UUID.randomUUID().toString()` caso seja um novo cadastro.
    
- [ ] Implementar o cálculo de Custo Médio Ponderado na Controller: Receber os dados de entrada, calcular a fórmula $CMP = \frac{(QtdAtual \times CustoAtual) + (QtdNova \times PrecoNovo)}{QtdAtual + QtdNova}$ e enviar os novos valores diretamente para a query de atualização do DAO.
    
- [ ] Implementar o gerador de parcelas na Controller de Vendas:
    
    - [ ] Dividir matematicamente o valor total pelo número de parcelas informadas pelo usuário.
        
    - [ ] Aplicar a sobra de arredondamento (centavos) na última iteração do laço de criação das parcelas.
        
    - [ ] Calcular as datas de vencimento somando a constante de tempo nativa do sistema em milissegundos e salvar a lista no DAO.
        
- [ ] Implementar o gatilho de baixa na Controller de Recebimentos:
    
    - [ ] Atualizar a `InstallmentEntity` específica preenchendo a data atual (em Long).
        
    - [ ] Consultar o DAO para verificar se restam parcelas em aberto daquela venda e, caso não existam, emitir o update na `SaleEntity` alterando o status para FINALIZADA.
        

### 5. Validação e Testes de Integridade (JUnit Nativo)

Os testes validarão as regras matemáticas e o comportamento esperado, sem depender de ambientes complexos.

- [ ] Escrever funções de teste unitário (puro Kotlin/JUnit) para a matemática do Custo Médio Ponderado.
    
- [ ] Escrever testes unitários verificando a divisão de valores e o comportamento do arredondamento na geração de parcelas simuladas.
    
- [ ] Validar a regex de limpeza do número de telefone antes de testar a inserção simulada da entidade Cliente.