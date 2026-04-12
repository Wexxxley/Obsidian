Estratégia "vanilla" consiste em remover bibliotecas de terceiros (como frameworks de Injeção de Dependência, ex: Hilt ou Koin) e reduzir a complexidade interna do Room.

Para isso, os identificadores únicos serão tratados nativamente como `String` no banco de dados (gerados via `java.util.UUID.randomUUID().toString()`), e as datas serão salvas diretamente como `Long` (timestamps). Isso elimina a necessidade de criar conversores complexos, mantendo o banco de dados leve. Além disso, a arquitetura dispensará a camada de Serviço, executando as regras diretamente nos Controllers ou ViewModels.
### Definição de Enums

Os enums representam o domínio do sistema e serão salvos no banco de dados.
- **ItemType:** PRODUTO ou SERVIÇO.
- **UnitType:** UNIDADE, KG, LITRO, METRO.
- **CategoryType:** ITENS ou DESPESAS.
- **SaleStatus:** ORÇAMENTO, PENDENTE, ATRASADA, FINALIZADA, CANCELADA.
- **InstallmentStatus:** PENDENTE, PAGA, ATRASADA.
- **PaymentMethod:** DINHEIRO, PIX, DÉBITO, CRÉDITO, FIADO.

### 1. Infraestrutura e Configuração Base (Vanilla)

- [ ] Configurar exclusivamente as dependências essenciais do Room (Runtime, KTX) e KSP no arquivo `build.gradle` do módulo.
    
- [ ] Criar a classe `TypeConverters` restrita apenas à conversão dos Enums para `String` (e vice-versa), utilizando a propriedade `.name` nativa do Kotlin.
    
- [ ] Implementar a classe abstrata `AppDatabase` configurando a versão inicial e registrando o `TypeConverters` dos Enums.
    
- [ ] Implementar a instanciação manual do banco de dados (Singleton) utilizando uma classe base que herda de `Application` no Android, provendo o `AppDatabase` globalmente sem frameworks externos de injeção de dependência.
    

### 2. Modelagem das Entidades 

ids serao uuid mas o tipo nativo utilizado será `String` (VARCHAR).

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

### 3. Implementação dos DAOs e Queries de Negócio

- [ ] Implementar `CategoryDao` com suporte a filtros básicos por `CategoryType`.
    
- [ ] Implementar `ClientDao` para inserção, atualização e busca por nome.
    
- [ ] Implementar `ProductDao` contendo a query SQL nativa para atualizar o saldo e custo médio de forma atômica.
    
- [ ] Criar `InstallmentDao` focando no cruzamento de dados:
    
    - [ ] Consulta (`JOIN` nativo) para buscar todas as parcelas pendentes ou atrasadas de um `clientId`.
        
    - [ ] Função de agregação (`SUM`) nativa do SQLite para retornar o débito total do cliente.
        
- [ ] Implementar `SaleDao` utilizando a anotação `@Relation` estritamente para agrupar a `SaleEntity` com suas respectivas listas de `SaleItemEntity` e `InstallmentEntity`.
    

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