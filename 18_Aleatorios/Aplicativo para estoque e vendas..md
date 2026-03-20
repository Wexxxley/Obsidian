

---
Solução **totalmente local** (executada e armazenada apenas no celular do cliente), a arquitetura ideal é o uso de um banco de dados **SQLite** embarcado. O "backend" será, na verdade, uma camada de serviço dentro do código do app.
### **[RF01] Cadastrar Produto/Serviço**

**Descrição:** Como Microempreendedor, quero registrar itens (produtos ou serviços) para compor meu catálogo.
    
**Fluxo Principal:** 
	1. Usuário acessa "Produtos/Serviços".
    2. Seleciona Tipo: Produto (gerencia estoque) ou Serviço (não gerencia estoque).
    3. Insere Nome, Preço de Custo (Referência) e Preço de Venda.
    4. (Opcional) Seleciona uma categoria de item.
    5. Salva o registro.
    
**Fluxos Alternativos:** 
- FA01: Campos obrigatórios em branco (O sistema impede e sinaliza o campo).

Mensagens do Sistema: 
- MSG01: "Produto cadastrado com sucesso."
    
**Critérios de Aceitação:** Se "Produto", inicia com quantidade zero. Se "Serviço", controle de estoque fica bloqueado.    

---
### **[RF02] Editar produto**

Como Microempreendedor, quero alterar as informações de um produto já cadastrado.

**Pré-requisito:** Produto deve estar cadastrado [RF01].

**Fluxo**
1. Usuário seleciona um produto na lista. 
2. Clica em "Editar". 
3. Altera as informações desejadas. 
4. Salva as alterações

**Mensagem do sitema:** MSG01: "Alterações salvas com sucesso."

**Critérios de aceitação:** As novas informações devem refletir imediatamente no catálogo e futuras vendas.

---
### **[RF03] Cadastrar Categoria**

**Descrição:** Criar categorias para organizar itens e despesas.
    
**Fluxo Principal:**
1. Usuário acessa o menu de "Categorias".
2. Define se a categoria é para **Itens** ou **Despesas**.
3. Insere o nome e salva.

**Extensão:** **Tela Informativa "O que são categorias?"**. Antes de criar as primeiras categorias, o sistema explica que categorias bem definidas ajudam a descobrir onde o dinheiro está sendo gasto (ex: Diferença entre _Insumos_ e _Manutenção_).

**Critérios de Aceitação:** Categorias de itens aparecem no [RF01] e de despesas no [RF13].  

---
### **[RF04] Registrar Entrada de Estoque (Custo Médio)**

**Descrição:** Adicionar quantidades informando o valor pago para recalcular o custo médio.

**Pré-requisito:** Item ser do tipo "Produto".

**Fluxo Principal:**
1. Usuário seleciona o produto e clica em "Adicionar Estoque".
2. Informa a **Quantidade Recebida** e o **Preço de Custo Unitário** atual.
3. O sistema atualiza o saldo total e recalcula o **Custo Médio Ponderado**.
$$CMédio = \frac{(\text{Qtd em Estoque} \times \text{Custo Médio Atual}) + (\text{Qtd Nova} \times \text{Preço de Compra Novo})}{\text{Qtd em Estoque} + \text{Qtd Nova}}$$
4. Confirma a operação.

**Camada de Extensão:** Modal informativo explicando que o Custo Médio Ponderado evita que o empreendedor perca dinheiro em épocas de inflação ou aumento de fornecedor.

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

Descrição: Como Microempreendedor, quero atualizar os dados de contato ou endereço de um cliente já cadastrado.

**Pré-requisito**: Cliente deve estar cadastrado [RF05].

1. Usuário pesquisa e seleciona o cliente. 
2. Altera os campos necessários (Telefone, Endereço, etc). 
3. Salva a edição.

**Critérios de aceitação:** Os dados atualizados devem ser exibidos no perfil do cliente e em novos comprovantes de venda.

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

**Fluxos Alternativos:** FA01: Pagamento Misto: Usuário seleciona dois métodos (ex: R$ 50 Pix e R$ 20 Dinheiro).

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
### **[RF1] Relatório de Lucratividade e Diagnóstico de Saúde**

**Descrição:** Como Microempreendedor, quero visualizar meu lucro líquido mensal acompanhado de uma análise simplificada sobre a viabilidade do meu negócio.

**Fluxo Principal:**
1. Usuário acessa a aba "Relatórios".
2. Seleciona o período (Mês/Ano).
3. O sistema calcula o Lucro Real baseado apenas em **Vendas Finalizadas (Pagas)**.
 $$Lucro = (\text{Vendas Pagas}) - (\text{Custo Médio dos Itens Vendidos}) - (\text{Despesas do Negócio})$$


---
### **Roteiro entrevista**

1. Hoje, quando você vende algo ou paga uma conta do seu negócio, você anota? você tem controle dos gastos e lucros do seu negócio? 
    
2. Você possui clareza sobre o lucro real do seu negócio ao final do mês, subtraindo custos de aquisição e despesas operacionais?
    
3. Além do custo do produto, você registra gastos fixos (aluguel, luz) ou variáveis (embalagens, frete) separadamente para entender o peso de cada um no seu negócio?
    
4. Quais são os principais obstáculos (falta de tempo, esquecimento, complexidade) que impedem o registro imediato e diário de todas as transações?
    
5. Você costuma misturar o dinheiro do seu negócio com o seu dinheiro pessoal?
    
6. Você utiliza notas promissórias ou algum tipo de recibo físico para formalizar essas dívidas?
    
7. No caso de vendas não pagas no ato, quais informações você anota para garantir a cobrança (nome, data de vencimento, parcelas pagas)?
    
8. Você identifica facilmente quais clientes possuem parcelas em atraso e qual o montante total que você tem para receber?
    
9. Você mantém um histórico de compras por cliente para oferecer promoções ou realizar cobranças?
    
10. Você acha que um app descomplicado onde você poderia fazer suas vendas, anotar vendas, selecionar formas de pagamento, ver as parcelas a serem pagas, as datas a serem recebidas, de forma offline, na palma da sua mão seria prático para vc?