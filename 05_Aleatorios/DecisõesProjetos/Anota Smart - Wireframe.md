

---

Wireframe Textual, estruturado formalmente para servir de guia absoluto para o desenvolvimento da interface e do fluxo de dados.

Cores para o wireframe: cinza 1 (escuro), cinza 2(tonalidade média), cinza 3 (claro)

Use icones simples, e somente as caixas (sem curvas) de conteudo com texto generico. 

App mobile. 9:16
### **1. Estrutura de Navegação e Componentes Fixos**
#### Top App Bar
- **Ícone de Menu (Lado Esquerdo):** Três traços que disparam o _Navigation Drawer_.
- **Identidade Visual (Centro):** Círculo de avatar exibindo a foto do microempreendedor ou o logotipo da empresa.
- **Carrinho de Vendas (Lado Direito):** Ícone de carrinho de compras com um contador numérico, indicando o total de itens atualmente no rascunho da venda.

#### Navigation Drawer (Menu Lateral)
- **Cabeçalho:** Foto e nome do usuário/empresa.
- **Categorias:** Tela de gerenciamento para criar categorias de "Itens" ou "Despesas". 
- **Tema claro/escuro**
- **Inserir chave pix**:
- **Sobre:** Informações da versão do software.
#### Bottom Navigation Bar
- **Venda:** O ponto central de operação (PDV).
- **Produtos**: local onde vai ser possivel gerenciar estoque
- **Pedidos**: area onde fica o hisotrico de vendas e o gerenciamento de valores a receber.
- **Clientes:** Gestão de contatos e histórico devedor.
- **Despesas**: local para cadastrar despesas fora da aquisição de estoque, como manutenção, transporte, insumos, agua, energia...
- **Mais:** Submenu contendo os Relatórios de Lucratividade e a Central de Ajuda.

### **2. Detalhamento da Tela de Venda**
#### Seção A: Entrada e Busca
- **Campo de Pesquisa:** Input de texto com lupa para filtrar a LazyVerticalGrid (3 colunas) de produtos pelo nome.
- **Botão de Venda Avulsa:** Um card destacado para itens não cadastrados, exigindo Nome, Preço de Custo e Preço de Venda.
- **LazyRow** com categorias de produtos para filtrar abaixo do campo de pesquisa.

#### Seção B: Catálogo de Seleção (Grid)
- **Cards de Produto:** As informaçoes do card aparecem como colunas. Exibem a imagem (800x800px), nome, preço de venda e saldo atual em estoque indicando a medida correspondente. 3 colunas
    
- **Modal de Quantidade:**
	- Se a unidade for Unidade: Teclado numérico apenas para inteiros.
	- Se a unidade for **Kg, Gramas, Litro ou Metro**: Teclado com ponto flutuante.
	- **Modal Alerta de Estoque:** Caso a quantidade desejada supere o saldo, um texto em vermelho indica "Estoque Insuficiente".
#### Botões para carrinho
- Em vez de depender apenas do ícone no topo, utilize uma barra fixa (que sobrepoe os produtos) que aparece assim que o primeiro item é adicionado. Logo acima da `BottomNavigationBar`.
- Lado esquerdo: "Total: R$ 00,00" e a quantidade de itens.
- Lado direito: Botão de ação escrito **"VER CARRINHO"**.
#### Carrinho e Checkout
- **LazyColumn do Carrinho:** Exibe cada item, sua quantidade, preço, Ícone de "Lápis" para reabrir o Modal de Quantidade e ícone de "Lixeira" (na cor vermelha) para remoção imediata do item. 
- **Valor Total:** Exibido em destaque no canto inferior esquerdo.
- Botao "**Finalizar venda**" no canto inferior direito sobrepondo os elementos se preciso.

#### Tela Seleção de pagamento

- **Seleção de Cliente (Obrigatório para Fiado):**
    - Um campo de busca que consulta a lista de clientes cadastrados (RF05). Caso o cliente n exista, deve aparecer um botao para cadastrar cliente. Ao clicar em adicionar, abre-se um pequeno formulário (Overlay) solicitando apenas **Nome** e **Telefone**.
    - Se o usuário selecionar "Parcelado" ou "Fiado" sem escolher um cliente, o sistema deve exibir um alerta bloqueando a operação (FA01 do RF10).
        
- **Bloco A: Pagamento Imediato (À Vista)**
    - Três botões grandes e táteis: **Dinheiro**, **PIX** e **Débito**. Caso a opção seja dinheiro, um modal ira se abrir para informar o dinheiro recebido e informar o troco.
    - Ao clicar em um deles, o sistema seleciona o método e destaca a borda do botão.
    - O status da venda é definido internamente como **"Finalizada"**.
        
- **Bloco B: Pagamento Futuro (Parcelado/Fiado)**
    - Botão destacado: **"Parcelar / Fiado"**.
    - **Validação Ativa (FA01 do RF10):** Se este botão for acionado sem um cliente selecionado, o sistema deve exibir um alerta visual  bloqueando o avanço.
    - Se tudo ok, vai ser aberto um modal de parcelas.

- **Modal de parcelas:** 
	- **Seletor de Quantidade de Parcelas:** Um componente de incremento/decremento (botões `+` e `-`). Ao alterar o número de parcelas, o sistema divide automaticamente o valor total da venda e exibe o valor de cada prestação. "3 parcelas de R$ 50,00".
        
	- **Definição de Datas de Vencimento:**
	    - **Data da Primeira Parcela:** Um campo de seleção de data (Date Picker) que, por padrão, sugere 30 dias após a data atual. O resto das datas serao consideradas de 30 em 30 dias.    
	        
- **Botão Finalizar**: Fixo no rodapé da tela. Só é habilitado após a seleção de um método de pagamento válido. Ao clicar app deve exibir um **Overlay de Sucesso**:
	- **Animação:** Um ícone de check animado ocupando o centro da tela.
	- **Resumo Rápido:** "Venda de R$ 150,00 finalizada com sucesso!".
	- Botão voltar para tela inicial.

![](../../attachments/Pasted%20image%2020260324143128.png)

### **3. Tela de Produtos**

#### **A. Área de Cabeçalho e Filtros**
- **Barra de Busca:** Campo de texto com bordas arredondadas e ícone de lupa. O texto inserido filtra a `LazyVerticalGrid` em tempo real pelo nome do item.
- **LazyRow de Categorias**
	Note que a barra de busca e a row de cateogiras ja existe na tela de vendas, basta copiar e colar aqui
- **Contador de Itens:** Pequeno texto discreto indicando o total de itens listados (Ex: "42 itens encontrados").
    
#### **B. Catálogo de Itens (LazyVerticalGrid - 3 Colunas)**

Cada card de produto/serviço segue uma estrutura de coluna vertical para otimizar o espaço:
- **Topo do Card:** Imagem quadrada (800x800px).
- **Meio do Card (Informações):**
    - **Nome:** 
    - **Preço de Venda:**R$ 25,00.
    - **Saldo e Unidade:** Texto indicando a quantidade e a medida 
        
- **Base do Card (Ações):**
    - **Botão "Adicionar" (Apenas para Produtos):** Ícone de "+" que abre o modal de entrada de estoque.
    - **Ícone de "Lápis":** No canto superior direito da imagem para acesso rápido à edição.

#### **C. Fluxo de Adição (Menu e Modais)**

- **Botão Flutuante (FAB):** Um botão com o símbolo "+" no canto inferior direito da tela.
- **Overlay de Escolha:** Ao clicar no FAB, surgem dois botões menores acima dele: "Novo Produto" e "Novo Serviço".
- **Modal de Novo Produto:**
    - Campo para Upload de Imagem.
    - Campo de Texto: Nome.
    - FlowRow: Seleção de Categorias.
    - Campo Numérico: Preço de Venda.        
    - Campo Numérico (Referência): Preço de Custo Inicial.
    - Dropdown: Unidade de Medida (Unidade, Kg, Gramas, Litro, Metro).
        
- **Modal de Novo Serviço:**
    - Campo para Upload de Imagem.
    - Campo de Texto: Nome.
    - FlowRow: Seleção de Categoria.
    - Campo Numérico: Preço de Venda.

#### **D. Modal de Gestão de Entrada**

Acionado pelo botão "Adicionar" nos cards de produtos:
- **Informativo:** Exibe o "Custo Médio Atual" para comparação.
- **Entrada de Dados:**
    - Campo: Quantidade Recebida (aceita decimais para Kg/Metro).
    - Campo: Novo Preço de Custo Unitário.
        
- **Rodapé do Modal:** Botão "Confirmar Entrada".

### **4. Tela de Pedidos 

### A. Navegação por Abas

- **Aba "Vendas":** Lista cronológica de todos os registros (Finalizadas, Pendentes, Canceladas).
    
- **Aba "A Receber":** Lista filtrada apenas por vendas com status "Pendente" ou "Atrasada".

## B. Design do Card de Pedido

- **Cabeçalho:** Nome do Cliente, se houver e data/Hora.
- **Corpo:** Valor Total da venda e ícone indicando o método de pagamento (PIX, Dinheiro, etc).
- **Status Visual:** Uma etiqueta (Tag) colorida no canto:
    - **Verde:** Finalizada.
    - **Amarelo:** Pendente (Fiado/Parcelado).
    - **Vermelho:** Atrasada (Vencimento ultrapassado).

## C. Detalhe e Baixa de Parcelas

Ao clicar em um pedido "Pendente":
- Exibe a lista de parcelas geradas no checkout. 
- Cada linha mostra: "Parcela X - R$ XX,XX - Vencimento DD/MM".
- **Botão "Baixar":** Localizado ao lado de cada parcela pendente. Ao clicar, o status daquela parcela muda para "Paga".

### **5. Tela de Clientes**

- **Lista de Clientes (LazyColumn):** Exibe foto (se houver), nome e telefone.
- **Perfil do Cliente:** Ao clicar, abre os detalhes com:
    - **Botão WhatsApp:** Abre conversa direta usando o número limpo.
    - **Histórico de Compras:** Lista de todos os pedidos vinculados àquele UUID.
        
- **Cadastro:** Nome, Telefone e Endereço.
    



---

## **7. Tela "Mais" (Submenu)**

- **Central de Ajuda:**
    - Grid de cards com miniaturas e títulos de tutoriais (ex: "Como cadastrar produtos", "Como fazer uma venda fiada").
    - Ao clicar, redireciona para o link do YouTube correspondente


## **Estrutura de Dados e Persistência (Back-end Local)**

Para suportar essa interface no banco de dados SQLite (Room), a lógica deve seguir estas regras:

- **Vínculo de UUID:** A venda parcelada armazena o `UUID` do cliente para permitir a gestão de cobrança posterior.
    
- **Tabela de Parcelas:** Deve existir uma tabela relacionada à venda (`SaleEntity`) chamada `InstallmentEntity`, contendo:
    
    - `saleId` (chave estrangeira).
        
    - `dueDate` (data de vencimento).
        
    - `amount` (valor da parcela).
        
    - `status` (Pendente ou Paga).
        
- **Registro de Custo Médio:** No momento da confirmação, o sistema captura o **Custo Médio Ponderado** atual dos produtos para que, mesmo que a dívida demore meses para ser paga, o lucro calculado no relatório [RF13] seja baseado no custo da época da venda.
    

---
        
- **Botão de confirmação**: Fixo no rodapé da tela. Só é habilitado após a seleção de um método de pagamento válido.

---

### **3. Detalhamento da Tela de Relatórios e Ajuda**

- **Filtro Temporal:** Seleção de Mês/Ano para consulta.
    
- **Métricas de Lucro Real:**
    - Soma de todas as "Vendas Finalizadas" (Pagas).
    - Subtração automática do Custo Médio Ponderado dos itens vendidos (CMV).
    - Subtração das "Despesas do Negócio" cadastradas via categoria de despesas.
        


![300](../../attachments/Pasted%20image%2020260324090925.png)
![300](../../attachments/Pasted%20image%2020260324090952.png)
![](../../attachments/Pasted%20image%2020260324091025.png)
![300](../../attachments/Pasted%20image%2020260324090812.png)
