
---

### 1. Requisitos funcionais INICIAS

1. Cadastrar produto, inicialmente com qtd zero. Posteriormente é pra ter a possibilidade fazer "o descarregaento dos produtos novos"(n sei o nome técnico) a atribuir as quantidades novas de produto
2. 3. Quero poder cadastrar clientes (nome, ft, numero, end) 
3. Quero poder fazer vendas, quero ter a possibilidade de selecionar produtos, colocar no carrinho e vender. E tbm quero ter a possibilidade de adicionar um venda "avulsa". seleciono o custo do produto, o preço e vendo sem selcionar um produto em si. (para caso de venda de produto fora do estoque ou peças muito específicas.) Adicionar um cliente associado a venda ou nao.
4. As formas de pagmento sao algo complicado, mas por enquanto, so quero conseguir selecionar a forma de pagamento, associar ao cliente ou n. status do pagamento, fiaod e parcelado sao algo que preciso fazer mas por enquanto n sei como
5. Quero poder cadastrar despesas do comercio, tipo reforma, compra de itens decorativos, etc (o que for de fora dos custos dos produtos)
6. 3. Quero conseguir saber o quanto de lucro tive(retirando os custos dos produtos) de um periodo, ultimos 5, 10, 30 dias e etc.

---
### **[RF01] Cadastrar Produto**

**Descrição:** Como Microempreendedor, quero registrar um produto (nome, categoria e preço para compor meu catálogo.

**Pré-requisito:** N/A.

**Fluxo Principal:**
1. Usuário acessa a tela de "Produtos".
2. Clica no botão de adicionar.
3. Insere as informações
4. (Opcional) Seleciona uma categoria.
5. Salva o registro.
    
**Fluxos Alternativos:** 
- **FA01:** Campos obrigatórios em branco (O sistema impede e sinaliza o campo).
    
**Mensagens do Sistema:**
- **MSG01:** "Produto cadastrado com sucesso."
    
**Critérios de Aceitação:**
- O produto deve ser listado com quantidade zerada por padrão após o cadastro.

---
### **[RF02] Registrar Entrada de Estoque**

**Descrição:** Como Microempreendedor, quero adicionar quantidades a um produto já cadastrado para atualizar o saldo físico.

**Pré-requisito:** Produto já deve estar cadastrado.

**Fluxo Principal:**
1. Usuário seleciona um produto existente.
2. Clica em "Adicionar Estoque".
3. Informa a quantidade recebida.
4. Confirma a operação.
    
**Fluxos Alternativos:** 
- **FA01:** Quantidade informada é negativa (Sistema bloqueia e pede valor positivo).
    
**Mensagens do Sistema:**
- **MSG01:** "Estoque atualizado com sucesso."
    
**Critérios de Aceitação:**    
- O saldo atual do produto deve ser atualizado somando o valor novo ao valor antigo.

---
### **[RF03] Cadastrar Cliente**

**Descrição:** Como Microempreendedor, quero salvar os dados de contato dos clientes para associá-los às vendas.

**Pré-requisito:** N/A.

**Fluxo Principal:**
1. Usuário acessa a tela de "Clientes".
2. Insere Nome, Telefone e Endereço.
3. (Opcional) Anexa uma foto do cliente.
4. Clica em "Salvar".
    
**Mensagens do Sistema:**
- **MSG01:** "Cliente salvo com sucesso."
    
**Critérios de Aceitação:**
- O cliente deve aparecer na lista de seleção durante a finalização de uma venda.

---
### **[RF04] Adicionar Itens ao Carrinho de Venda**

**Descrição:** Como Microempreendedor, quero selecionar produtos do estoque para iniciar o processo de uma venda.

**Pré-requisito:** Existência de produtos cadastrados com estoque.

**Fluxo Principal:**
1. Usuário inicia uma "Nova Venda".
2. Pesquisa e seleciona um produto.
3. Define a quantidade para venda.
4. Adiciona ao carrinho.
5. Repete o processo para outros itens, se necessário.
    
**Critérios de Aceitação:**
- O sistema deve mostrar o subtotal parcial conforme os itens são adicionados.

---
### **[RF05] Realizar Venda Avulsa**

**Descrição:** Como Microempreendedor, quero registrar a venda de um item que não está no meu cadastro de estoque (peças específicas ou serviços).

**Pré-requisito:** N/A.

**Fluxo Principal:**
1. Usuário seleciona a opção "item Avulso" na tela de vendas.
2. Digita manualmente o Preço de Custo e o Preço de Venda.
3. Adiciona ao carrinho.

**Mensagens do Sistema:**
- **MSG01:** "Item avulso adicionado."
    
**Critérios de Aceitação:**    
- Essa venda não deve descontar unidades de nenhum produto do cadastro fixo.

---
### **[RF06] Finalizar Venda e Definir Pagamento**

**Descrição:** Como Microempreendedor, quero fechar o carrinho, escolher a forma de pagamento e associar (ou não) a um cliente.

**Pré-requisito:** Ter itens no carrinho [RF04 ou RF05].

**Fluxo Principal:**
1. Usuário clica em "Finalizar Venda".
2. Seleciona a Forma de Pagamento (Dinheiro, PIX, Cartão).
3. Seleciona o Status (Pago ou Pendente).
4. (Opcional) Seleciona um Cliente da lista.
5. Confirma a venda.
    
**Fluxos Alternativos:**    
- **FA01:** Finalizar sem selecionar cliente (Sistema permite como "Consumidor Final").
    
**Critérios de Aceitação:**    
- O estoque dos produtos envolvidos (se houver) deve ser baixado após a confirmação.  

---
### **[RF07] Registrar Despesa Externa**

**Descrição:** Como Microempreendedor, quero anotar gastos que não são mercadorias (luz, internet, sacolas) para controlar minhas saídas.

**Pré-requisito:** N/A.

**Fluxo Principal:**
1. Usuário acessa "Despesas".
2. Digita a Descrição e o Valor.
3. Clica em "Salvar".

**Critérios de Aceitação:**
- A despesa deve ser subtraída do lucro líquido nos relatórios.

---
### **[RF08] Consultar Lucro por Período**

**Descrição:** Como Microempreendedor, quero ver o desempenho financeiro dos meses.

**Pré-requisito:** Existência de vendas registradas.

**Fluxo Principal:**
1. Usuário acessa "Relatórios".
    
2. O sistema calcula: $\text{Total Vendido} - \text{Custo Total das Peças} - \text{Despesas}$ para os meses com registro.
    
**Critérios de Aceitação:**
- O sistema deve exibir o valor do "Lucro Real" de forma clara.
    



### Ideias pro futuro

Adicionar categorias, e essas cotegorias podem ser associadas a produtos para facilitar buscas, retornar relatorios e etc.