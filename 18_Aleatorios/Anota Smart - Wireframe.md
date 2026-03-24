

---

Wireframe Textual, estruturado formalmente para servir de guia absoluto para o desenvolvimento da interface e do fluxo de dados.

Cores para o wireframe: cinza 1 (escuro), cinza 2(tonalidade média), cinza 3 (claro)

Use icones simples, e somente as caixas (sem curvas) de conteudo com texto generico. 
### **1. Estrutura de Navegação e Componentes Fixos**
#### Top App Bar

- **Ícone de Menu (Lado Esquerdo):** Três traços que disparam o _Navigation Drawer_.
- **Identidade Visual (Centro):** Círculo de avatar exibindo a foto do microempreendedor ou o logotipo da empresa.
- **Carrinho de Vendas (Lado Direito):** Ícone de carrinho de compras com um contador numérico, indicando o total de itens atualmente no rascunho da venda.

#### Navigation Drawer (Menu Lateral)
- **Cabeçalho:** Nome do usuário/empresa.
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

### **2. Detalhamento da Tela de Venda **
#### **Seção A: Entrada e Busca**

- **Campo de Pesquisa:** Input de texto com lupa para filtrar a LazyVerticalGrid (4 colunas) de produtos pelo nome.
    
- **Botão de Venda Avulsa:** Um card destacado para itens não cadastrados, exigindo Nome, Preço de Custo e Preço de Venda.
    

## **Seção B: Catálogo de Seleção (Grid)**

- **Cards de Produto:** Exibem a imagem (processada em 800x800px via Coil/Glide), nome, preço de venda e saldo atual em estoque.
    
- **Seletor de Quantidade Fracionada [RF07]:** Ao tocar no card, um diálogo sobrepõe a tela:
    
    - Se a unidade for **Unidade ou Pinto**: Teclado numérico apenas para inteiros.
        
    - Se a unidade for **Kg, Gramas, Litro ou Metro**: Teclado com ponto flutuante (decimal) habilitado.
        
    - **Alerta de Estoque:** Caso a quantidade desejada supere o saldo, um texto em vermelho indica "Estoque Insuficiente" (FA01 do RF07).
        

## **Seção C: Carrinho e Checkout [RF09/RF10]**

- **Lista do Carrinho:** Exibe cada item, sua quantidade fracionada e o subtotal parcial calculado em tempo real.
    
- **Vinculação de Cliente:** Um seletor "Vincular Cliente" (obrigatório se a venda for Pendente/Fiada).
    
- **Seleção de Pagamento:**
    
    - **Botão À Vista:** Abre opções de Dinheiro, PIX ou Débito. Finaliza como status "Finalizada".
        
    - **Botão Parcelado/Fiado:** Abre calendário para definir datas de vencimento. Finaliza como status "Pendente".
        
- **Botão Finalizar:** Grande, na cor verde, executando a baixa automática no estoque e gerando o registro financeiro.
    

---

### **3. Detalhamento da Tela de Relatórios e Ajuda**

- **Filtro Temporal:** Seleção de Mês/Ano para consulta.
    
- **Métricas de Lucro Real:**
    - Soma de todas as "Vendas Finalizadas" (Pagas).
    - Subtração automática do Custo Médio Ponderado dos itens vendidos (CMV).
    - Subtração das "Despesas do Negócio" cadastradas via categoria de despesas.
        

