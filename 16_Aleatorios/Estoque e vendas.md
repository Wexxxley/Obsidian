

---
### **[RF01] Cadastrar Produto/Serviço**

**Descrição:** Como Microempreendedor, quero registrar itens (produtos ou serviços) para compor meu catálogo.

**Pré-requisito:** N/A.

**Fluxo Principal:**
1. Usuário acessa a tela de "Produtos/Serviços".
2. Seleciona o **Tipo**: Produto (gerencia estoque) ou Serviço (não gerencia estoque).
3. Insere Nome, Preço de Custo (Referência) e Preço de Venda.
4. (Opcional) Seleciona uma categoria de item.
5. Salva o registro.

**Fluxos Alternativos:**    
- **FA01:** Campos obrigatórios em branco (O sistema impede e sinaliza o campo).  

**Mensagens do Sistema:**    
- **MSG01:** "Item cadastrado com sucesso."
    
**Critérios de Aceitação:**    
- Se for "Produto", inicia com quantidade zero. Se for "Serviço", o controle de estoque fica bloqueado.

---
### **[RF02] Editar Produto/Serviço**

**Descrição:** Como Microempreendedor, quero alterar preços ou nomes de itens sem afetar as vendas que já foram realizadas.
**Pré-requisito:** Item cadastrado [RF01].
**Fluxo Principal:**
1. Usuário seleciona o item na lista e clica em "Editar".
2. Altera as informações desejadas (ex: novo Preço de Venda).
3. Salva as alterações.

---
### **[RF03] Cadastrar Categoria**

**Descrição:** Como Microempreendedor, quero criar categorias para organizar meus itens e minhas despesas.

**Fluxo Principal:**
1. Usuário acessa o menu de "Categorias".
2. Define se a categoria é para **Itens** ou **Despesas**.
3. Insere o nome e salva.
    
**Critérios de Aceitação:**
- Categorias de itens aparecem no [RF01] e categorias de despesas aparecem no [RF13].

---
### **[RF04] Registrar Entrada de Estoque (Custo de Entrada)**

**Descrição:** Como Microempreendedor, quero adicionar quantidades aos produtos informando o valor pago na nova remessa para recalcular o custo médio.

**Pré-requisito:** Item ser do tipo "Produto".

**Fluxo Principal:**
1. Usuário seleciona o produto e clica em "Adicionar Estoque".
2. Informa a **Quantidade Recebida** e o **Preço de Custo Unitário** atual.
3. O sistema atualiza o saldo total e recalcula o **Custo Médio Ponderado**.
$$CMédio = \frac{(\text{Qtd em Estoque} \times \text{Custo Médio Atual}) + (\text{Qtd Nova} \times \text{Preço de Compra Novo})}{\text{Qtd em Estoque} + \text{Qtd Nova}}$$
4. Confirma a operação.
    
**Mensagens do Sistema:**
- **MSG01:** "Estoque atualizado. Novo custo médio: R$ [Valor]."

---
### **[RF05] Cadastrar Cliente (Opcional)**

**Descrição:** Como Microempreendedor, quero salvar dados de contato dos clientes para facilitar vendas e cobranças.

**Fluxo Principal:**
1. Usuário acessa a tela de "Clientes". 
2. Insere Nome, Telefone e Endereço. 
3. (Opcional) Anexa uma foto do cliente. 
4. Clica em "Salvar"

**Mensagens do Sistema**
- MSG01: "Cliente salvo com sucesso.

**Critérios de Aceitação:**
- O telefone deve ser limpo (apenas números) para garantir o funcionamento da API do WhatsApp [RF14].

---
### **[RF06] Editar Cliente**

**Descrição:** Como Microempreendedor, quero manter os dados de contato dos meus clientes atualizados.

**Pré-requisito**: Cliente deve estar cadastrado [RF05].

**Fluxoprincipal**
1. Usuário pesquisa e seleciona o cliente. 
2. Altera os campos necessários (Telefone, Endereço, etc). 
3. Salva a edição.

**Critérios de Aceitação:**
- O telefone deve ser limpo (apenas números) para garantir o funcionamento da API do WhatsApp [RF14].

---
### **[RF07] Adicionar Itens ao Carrinho**

**Descrição:** Como Microempreendedor, quero selecionar produtos ou serviços para iniciar uma venda.

**Pré-requisito**: Existência de produtos cadastrados.

**Fluxo principal**
1. Usuário inicia uma "Nova Venda". 
2. Pesquisa e seleciona um produto. 
3. Define a quantidade para venda. 
4. Adiciona ao carrinho.

**Fluxos Alternativos:**
- **FA01: Estoque insuficiente:** O sistema exibe um alerta.

**Critérios de aceitação**: O sistema deve mostrar o subtotal parcial conforme os itens são adicionados.

---
### **[RF08] Realizar Venda Avulsa**

**Descrição:** Como Microempreendedor, quero registrar uma venda de algo fora do catálogo ou um serviço rápido.

**Pré-requisito**: N/A.

**Fluxo Principal:**

1. Usuário seleciona "Item Avulso".
2. Digita Nome, Preço de Custo (obrigatório) e Preço de Venda.
3. Adiciona ao carrinho.

**Mensagens do Sistema:** MSG01: "Item avulso adicionado."

**Critérios de Aceitação:** Essa venda não deve descontar unidades de nenhum produto cadastrado.

---
### **[RF09] Definir Pagamento à Vista (Dinheiro/Pix/Débito)**

**Descrição:** Como Microempreendedor, quero registrar pagamentos imediatos para finalizar a venda.

**Pré-requisito**: Itens no carrinho [RF07/RF08].

**Fluxo Principal:**
1. Usuário seleciona "Pagamento à Vista". 
2. Escolhe o método: Dinheiro, PIX ou Débito. 
3. O sistema captura o Preço de Custo Atual dos itens. 
4. Venda é salva como "Status: Finalizada (Paga)". 

**Mensagens do Sistema: MSG01:** "Pagamento registrado. Venda finalizada."

---
### **[RF10] Registrar Venda Parcelada ou Fiado**

**Descrição:** Como Microempreendedor, quero vender para receber depois, vinculando a dívida a um cliente.

**Pré-requisito:** Cliente selecionado e itens no carrinho.

**Fluxo Principal:**
1. Usuário seleciona "Parcelado" ou "Fiado".
2. Define as datas das parcelas.
3. O sistema grava o custo atual dos itens.
4. Status vira "Pendente".
    
**Fluxos Alternativos:**
- **FA01:** Cliente não selecionado (Bloqueia a venda).

**Mensagens do Sistema:**
- MSG01: "Atenção: Selecione um cliente para realizar venda fiada/parcelada."

---

### **[RF11] Gestão de Ciclo de Vida da Venda (Status)**

**Descrição:** Como Microempreendedor, quero gerenciar o progresso das vendas.

**Status:**
- **Orçamento:** Rascunho. Não altera estoque nem financeiro.
- **Pendente:** Pagamento incompleto (Fiado/Parcelado).
- **Atrasada:** Parcela com vencimento ultrapassado sem baixa.
- **Finalizada:** Tudo pago e estoque baixado.
- **Cancelada:** Estorna estoque e invalida valores.

---

### **[RF12] Gerenciar Recebimentos (Contas a Receber)**

**Descrição:** Como Microempreendedor, quero dar baixa nas dívidas conforme recebo os pagamentos.

**Fluxo Principal:**
1. Usuário acessa "Contas a Receber". 
2. Seleciona a dívida do cliente e clica em "Receber". 
3. Se o saldo devedor da venda chegar a zero, o sistema altera o status da venda para "Finalizada"
    

---
### **[RF13] Cadastrar Despesa Comercial**

**Descrição:** Como Microempreendedor, quero registrar gastos fixos ou variáveis categorizados.

**Fluxo Principal:**
1. Usuário insere Descrição, Valor, Data e seleciona uma Categoria de Despesa (ex: "Aluguel", "Insumos").
2. Salva o registro.

---

### **[RF14] Notificar Cobrança via WhatsApp (Integração API)**

**Descrição:** Como Microempreendedor, quero enviar lembretes de cobrança automáticos.

**Fluxo Principal:**
	....

---

### **[RF15] Relatório de Lucratividade**

**Descrição:** Como Microempreendedor, quero ver o lucro líquido mensal.

**Fórmula:**

$$Lucro = (\text{Vendas Recebidas}) - (\text{Custo de Aquisição dos Itens Vendidos}) - (\text{Despesas})$$


---
### IDEIAS FUTURAS

- Seleção de dois métodos de pagamento


