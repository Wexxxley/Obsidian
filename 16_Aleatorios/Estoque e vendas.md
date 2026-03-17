

---
### **[RF01] Cadastrar Produto/Serviço**

**Descrição:** Como Microempreendedor, quero registrar itens (produtos ou serviços) para compor meu catálogo.
    
**Fluxo Principal:** 
	1. Usuário acessa "Produtos/Serviços".
    2. Seleciona Tipo: Produto (gerencia estoque) ou Serviço (não gerencia estoque).
    3. Insere Nome, Preço de Custo (Referência) e Preço de Venda.
    4. (Opcional) Seleciona uma categoria de item.
    5. Salva o registro.
    
**Camada de Extensão:** Adição de um **Modal de Apoio "Como Precificar?"** ao lado do campo Preço de Venda, explicando que o valor deve cobrir o custo médio e as despesas fixas.
    
**Critérios de Aceitação:** Se "Produto", inicia com quantidade zero. Se "Serviço", controle de estoque fica bloqueado.    

### **[RF02] Editar Produto/Serviço**

**Descrição:** Como Microempreendedor, quero alterar preços ou nomes de itens sem afetar as vendas que já foram realizadas.

**Pré-requisito:** Item cadastrado [RF01].
**Fluxo Principal:**
1. Usuário seleciona o item na lista e clica em "Editar".
2. Altera as informações desejadas (ex: novo Preço de Venda).
3. Salva as alterações.

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

**Camada de Extensão:** Ao selecionar "Fiado", o sistema exibe uma **Dica de Saúde Financeira**: _"Sugerir parcelas menores aumenta sua chance de receber em dia!"_

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
### **[RF13] Cadastrar Despesa Comercial X pessoal**

**Descrição:** Como Microempreendedor, quero registrar gastos fixos ou variáveis categorizados.

**Camada de Extensão:** Inclusão de um checkbox: **"Esta despesa é do negócio ou retirada pessoal?"**.

**Modal Educativo:** Explicação sobre a importância de separar as contas da casa das contas da empresa.    

**Fluxo Principal:**
1. Usuário insere Descrição, Valor, Data e seleciona uma Categoria de Despesa (ex: "Aluguel", "Insumos").
2. Salva o registro.

---
### **[RF14] Notificar Cobrança via WhatsApp (Integração API)**

**Descrição:**  Enviar lembretes de cobrança automáticos. Sistema gera link de WhatsApp com template pronto.

---
### **[RF15] Relatório de Lucratividade e Diagnóstico de Saúde**

**Descrição:** Como Microempreendedor, quero visualizar meu lucro líquido mensal acompanhado de uma análise simplificada sobre a viabilidade do meu negócio.

**Fluxo Principal:**
1. Usuário acessa a aba "Relatórios".
2. Seleciona o período (Mês/Ano).
3. O sistema calcula o Lucro Real baseado apenas em **Vendas Finalizadas (Pagas)**.
4. O sistema apresenta o **Diagnóstico de Saúde** (Camada de Extensão).

**Detalhamento do Diagnóstico :** O sistema deve comparar três variáveis: **Receita**, **Custo de Mercadoria** e **Retiradas Pessoais (Pro-labore)**.
	**Lucro Negativo**: "Atenção: Suas despesas superaram suas entradas. Verifique se seu Preço de Venda [RF01] está cobrindo seus custos ou se houve muitas despesas extras este mês."
	**Retirada Pessoal > Lucro**: "Cuidado! Você está retirando para uso pessoal [RF13] mais do que a empresa lucrou. Isso pode deixar você sem dinheiro para repor o estoque amanhã."
	**Inadimplência Alta**: "Você tem R$ [Valor] em vendas 'Pendentes' ou 'Atrasadas'. Seu lucro seria maior se esses pagamentos estivessem em dia. Use o lembrete do WhatsApp [RF14]."
	**Lucro Positivo**: "Parabéns! Seu negócio deu lucro. Que tal separar uma parte para um fundo de reserva ou reinvestir em novos produtos?"
 $$Lucro = (\text{Vendas Pagas}) - (\text{Custo Médio dos Itens Vendidos}) - (\text{Despesas do Negócio})$$

---
### **[RF16] Glossário de Termos** 

**Descrição:** Como Microempreendedor, quero uma central de ajuda que traduza o "economês" para uma linguagem simples e prática do dia a dia.

Uma tela de lista acessível pelo menu principal ou pelos ícones de interrogação `(?)` espalhados pelo app.

1. **Custo Médio Ponderado:** "É o preço real que você pagou pela sua mercadoria. Se você comprou uma caixa de leite por R$ 4 e outra por R$ 5, seu custo médio é R$ 4,50. O app usa isso para você nunca ter prejuízo."    
2. **Capital de Giro:** "É o 'respiro' do seu negócio. É o dinheiro que você precisa ter guardado para comprar mercadoria antes mesmo de receber dos clientes que compraram fiado."
3. **Margem de Contribuição:** "É o que sobra de cada venda para pagar suas contas fixas (aluguel, luz) e formar seu lucro. Se a margem for pequena, você precisa vender muito para não fechar no vermelho."
4. **Inadimplência:** "É o famoso 'calote' ou atraso. É quando o dinheiro que deveria estar no seu caixa ainda está no bolso do cliente."
5. **Pró-labore:** "É o seu salário. Definir um valor fixo para você evita que você use o dinheiro da empresa para pagar contas de casa, o que é a maior causa de fechamento de negócios."
6. **Ponto de Equilíbrio:** "É o momento em que suas vendas pagaram exatamente todas as suas despesas. A partir daqui, tudo o que entrar é lucro de verdade."
