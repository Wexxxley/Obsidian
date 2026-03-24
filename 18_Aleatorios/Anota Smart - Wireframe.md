

---

Wireframe Textual, estruturado formalmente para servir de guia absoluto para o desenvolvimento da interface e do fluxo de dados.

Cores para o wireframe: cinza 1 (escuro), cinza 2(tonalidade média), cinza 3 (claro)

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
...
#### Bottom Navigation Bar
- **Catálogo:**
- **Venda:** O ponto central de operação (PDV).
- **Clientes:** Gestão de contatos e histórico devedor.
- **Mais:** Submenu contendo os Relatórios de Lucratividade e a Central de Ajuda.

---

## **2. Detalhamento da Tela de Venda (O Coração do App)**

Esta tela deve ser otimizada para operação rápida em campo.

## **Seção A: Entrada e Busca**

- **Campo de Pesquisa:** Input de texto com lupa para filtrar a `LazyVerticalGrid` de produtos pelo nome.
    
- **Scanner:** Botão flutuante ou ícone na barra de busca para ativar a câmera e ler códigos de barras, vinculando ao UUID do produto.
    
- **Botão de Venda Avulsa [RF08]:** Um card destacado para itens não cadastrados, exigindo Nome, Preço de Custo e Preço de Venda.
    

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

## **3. Detalhamento da Tela de Relatórios e Gestão [RF13]**

- **Filtro Temporal:** Seleção de Mês/Ano para consulta.
    
- **Métricas de Lucro Real:**
    
    - Soma de todas as "Vendas Finalizadas" (Pagas).
        
    - Subtração automática do Custo Médio Ponderado dos itens vendidos (CMV).
        
    - Subtração das "Despesas do Negócio" cadastradas via categoria de despesas.
        
- **Diagnóstico de Saúde:** Texto formal explicando se o lucro é suficiente para cobrir os custos fixos (aluguel, luz) baseados na entrevista do roteiro.
    

---

## **4. Prompt Estruturado para Geração de Interface (IA/Dev)**

> "Crie um protótipo de alta fidelidade para um App de Gestão Local (SQLite/Room) seguindo estas especificações:
> 
> 1. **Arquitetura de UI:** Utilize Scaffold com TopAppBar (Avatar central, Menu lateral à esquerda, Carrinho com badge à direita) e BottomNavigation com 4 abas (Catálogo, Venda, Clientes, Relatórios).
>     
> 2. **Lógica de Venda [RF07/RF08]:** Implemente uma tela de PDV que suporte busca por nome e venda avulsa. O seletor de quantidade deve aceitar `Double` (ponto flutuante) para unidades como Kg, Litro e Metro, e `Int` para unidades simples.
>     
> 3. **Gestão de Imagens:** Configure o carregamento de fotos de produtos e clientes a partir do `Internal Storage` (`context.filesDir`) utilizando caminhos de string armazenados no banco de dados. Use Coil para renderizar as imagens redimensionadas em cards.
>     
> 4. **Financeiro [RF09/RF10/RF13]:** Crie o fluxo de checkout que diferencie vendas 'Pagas' de 'Pendentes' (Fiado), vinculando obrigatoriamente um UUID de cliente às vendas pendentes. O relatório de lucro deve calcular o Lucro Real subtraindo o Custo Médio Ponderado e as despesas."
>     

---

**Deseja que eu detalhe agora a estrutura exata das tabelas do Room (entidades e relacionamentos) para garantir que o 'Custo Médio Ponderado' seja calculado corretamente em cada venda?**