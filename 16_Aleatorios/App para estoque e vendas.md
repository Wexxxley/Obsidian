
---

### 1. Requisitos funcionais INICIAS

1. Cadastrar produto, inicialmente com qtd zero. Posteriormente é pra ter a possibilidade fazer "o descarregaento dos produtos novos"(n sei o nome técnico) a atribuir as quantidades novas de produto
2. 3. Quero poder cadastrar clientes (nome, ft, numero, end) 
3. Quero poder fazer vendas, quero ter a possibilidade de selecionar produtos, colocar no carrinho e vender. E tbm quero ter a possibilidade de adicionar um venda "avulsa". seleciono o custo do produto, o preço e vendo sem selcionar um produto em si. (para caso de venda de produto fora do estoque ou peças muito específicas.) Adicionar um cliente associado a venda ou nao.
4. As formas de pagmento sao algo complicado, mas por enquanto, so quero conseguir selecionar a forma de pagamento, associar ao cliente ou n. status do pagamento, fiaod e parcelado sao algo que preciso fazer mas por enquanto n sei como
5. Quero poder cadastrar despesas do comercio, tipo reforma, compra de itens decorativos, etc (o que for de fora dos custos dos produtos)
6. 3. Quero conseguir saber o quanto de lucro tive(retirando os custos dos produtos) de um periodo, ultimos 5, 10, 30 dias e etc.

### **[RF01] Cadastrar Produto**

**Descrição:** Como Microempreendedor, quero registrar um produto (nome, categoria e preços) para compor meu catálogo.

**Pré-requisito:** N/A.

**Fluxo Principal:**
1. Usuário acessa a tela de "Produtos".
2. Clica no botão de adicionar.
3. Insere Nome, Preço de Custo e Preço de Venda.
4. (Opcional) Seleciona uma categoria.
5. Salva o registro.

**Fluxos Alternativos:**
- **FA01:** Campos obrigatórios em branco (O sistema impede e sinaliza o campo).
    
**Mensagens do Sistema:**    
- **MSG01:** "Produto cadastrado com sucesso."
    
**Critérios de Aceitação:**    
- O produto deve ser listado com quantidade zerada por padrão após o cadastro.

---
### **[RF02] Editar Produto**

**Descrição:** Como Microempreendedor, quero alterar as informações de um produto já cadastrado (como preço ou nome).

**Pré-requisito:** Produto deve estar cadastrado [RF01].

**Fluxo Principal:**

1. Usuário seleciona um produto na lista.
    
2. Clica em "Editar".
    
3. Altera as informações desejadas.
    
4. Salva as alterações.
    
    **Mensagens do Sistema:**
    

- **MSG01:** "Alterações salvas com sucesso."
    
    **Critérios de Aceitação:**
    
- As novas informações devem refletir imediatamente no catálogo e futuras vendas.
    

---

### **[RF03] Cadastrar Categoria de Produto**

**Descrição:** Como Microempreendedor, quero criar categorias (ex: "Camisetas", "Acessórios") para organizar meus produtos.

**Pré-requisito:** N/A.

**Fluxo Principal:**

1. Usuário acessa o menu de "Categorias".
    
2. Clica em "Nova Categoria".
    
3. Insere o nome da categoria.
    
4. Salva o registro.
    
    **Critérios de Aceitação:**
    

- A categoria criada deve aparecer como opção na tela de cadastro/edição de produtos.
    

---

### **[RF04] Registrar Entrada de Estoque**

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

### **[RF05] Cadastrar Cliente**

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

### **[RF06] Editar Cliente**

**Descrição:** Como Microempreendedor, quero atualizar os dados de contato ou endereço de um cliente já cadastrado.

**Pré-requisito:** Cliente deve estar cadastrado [RF05].

**Fluxo Principal:**

1. Usuário pesquisa e seleciona o cliente.
    
2. Altera os campos necessários (Telefone, Endereço, etc).
    
3. Salva a edição.
    
    **Critérios de Aceitação:**
    

- Os dados atualizados devem ser exibidos no perfil do cliente e em novos comprovantes de venda.
    

---

### **[RF07] Adicionar Itens ao Carrinho de Venda**

**Descrição:** Como Microempreendedor, quero selecionar produtos do estoque para iniciar o processo de uma venda.

**Pré-requisito:** Existência de produtos cadastrados.

**Fluxo Principal:**

1. Usuário inicia uma "Nova Venda".
    
2. Pesquisa e seleciona um produto.
    
3. Define a quantidade para venda.
    
4. Adiciona ao carrinho.
    
    **Fluxos Alternativos:**
    

- **FA01: Estoque insuficiente:** O sistema exibe um alerta, mas permite adicionar ao carrinho (Venda de estoque futuro).
    
    **Critérios de Aceitação:**
    
- O sistema deve mostrar o subtotal parcial conforme os itens são adicionados.
    

---

### **[RF08] Realizar Venda Avulsa**

**Descrição:** Como Microempreendedor, quero registrar a venda de um item que não está no meu cadastro de estoque.

**Pré-requisito:** N/A.

**Fluxo Principal:**

1. Usuário seleciona a opção "Item Avulso" na tela de vendas.
    
2. Digita obrigatoriamente o **Preço de Custo** e o **Preço de Venda**.
    
3. Adiciona ao carrinho.
    
    **Mensagens do Sistema:**
    

- **MSG01:** "Item avulso adicionado."
    
    **Critérios de Aceitação:**
    
- Essa venda não deve descontar unidades de nenhum produto cadastrado.
    
- O custo informado deve ser usado para o cálculo de lucro no [RF14].
    

---

### **[RF09] Definir Pagamento à Vista (Dinheiro/Pix/Débito)**

**Descrição:** Como Microempreendedor, quero registrar pagamentos imediatos para finalizar a venda.

**Pré-requisito:** Itens no carrinho [RF07/RF08].

**Fluxo Principal:**

1. Usuário seleciona "Pagamento à Vista".
    
2. Escolhe o método: Dinheiro, PIX ou Débito.
    
3. O sistema captura o **Preço de Custo Atual** dos itens (Snapshot).
    
4. Venda é salva como **"Status: Finalizada (Paga)"**.
    
    **Fluxos Alternativos:**
    

- **FA01: Pagamento Misto:** Usuário seleciona dois métodos (ex: R$ 50 Pix e R$ 20 Dinheiro).
    
    **Mensagens do Sistema:**
    
- **MSG01:** "Pagamento registrado. Venda finalizada."
    

---

### **[RF10] Registrar Venda Parcelada ou Fiado**

**Descrição:** Como Microempreendedor, quero registrar vendas para pagamento futuro vinculadas a um cliente.

**Pré-requisito:** Cliente selecionado [RF05] e itens no carrinho.

**Fluxo Principal:**

1. Usuário seleciona "Parcelado" ou "Fiado".
    
2. Define datas de vencimento e valores.
    
3. O sistema captura o **Preço de Custo Atual** dos itens (Snapshot).
    
4. Venda é salva como **"Status: Em Aberto"** ou **"Status: Pago Parcialmente"**.
    
    **Fluxos Alternativos:**
    

- **FA01: Cliente não selecionado:** O sistema bloqueia a finalização se o status for diferente de "Finalizada".
    
    **Mensagens do Sistema:**
    
- **MSG01:** "Atenção: Selecione um cliente para realizar venda fiada/parcelada."
    

---

### **[RF11] Gestão de Ciclo de Vida da Venda (Status)**

**Descrição:** Como Microempreendedor, quero gerenciar os estados da venda (Orçamento, Finalizada, Cancelada, Em Aberto).

**Fluxo Principal:**

1. **Orçamento:** Salva a lista sem baixar estoque.
    
2. **Finalizada:** Baixa estoque e entra no lucro real.
    
3. **Cancelada:** Estorna estoque e invalida financeiro.
    
    **Mensagens do Sistema:**
    

- **MSG01:** "Status atualizado. Itens estornados ao estoque." (Se cancelada).
    

---

### **[RF12] Atualizar Cadastro de Produto e Categorias**

**Descrição:** Como Microempreendedor, quero organizar meu catálogo editando nomes e vínculos.

**Fluxo Principal:** Usuário acessa o gerencial, altera o nome da categoria ou troca a categoria de um produto.

**Critérios de Aceitação:** A mudança de nome da categoria deve atualizar todos os produtos vinculados.

---

### **[RF13] Gerenciar Agenda de Recebimentos (Contas a Receber)**

**Descrição:** Como Microempreendedor, quero dar baixa em pagamentos pendentes.

**Fluxo Principal:**

1. Usuário acessa "Contas a Receber".
    
2. Seleciona a dívida do cliente e clica em "Receber".
    
3. Se o saldo devedor da venda chegar a zero, o sistema altera o status da venda para **"Finalizada"**.
    

---

### **[RF14] Relatório de Lucratividade Real vs. Prevista**

**Descrição:** Como Microempreendedor, quero visualizar o lucro do mês.

**Fluxo Principal:**

1. Sistema calcula o lucro baseado nos **Snapshots de Custo** salvos no momento das vendas.
    
2. Fórmula:
    
    $$Lucro = \text{Caixa Real} - (\text{Custo dos Itens Vendidos} + \text{Despesas})$$
    

---

### **[RF15] Desativar Registros (Segurança de Dados)**

**Descrição:** Como Microempreendedor, quero "apagar" produtos ou clientes sem perder o histórico financeiro.

**Fluxo Principal:**

1. Usuário clica em "Excluir".
    
2. Se o registro possuir vendas vinculadas, o sistema apenas o **Desativa** (esconde da lista de novos cadastros), mas mantém nos relatórios antigos.