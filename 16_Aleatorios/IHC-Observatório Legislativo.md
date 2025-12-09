
---
### **1. Contextualização**
Na era da informação digital, as redes sociais ampliaram drasticamente o alcance e a notoriedade dos debates políticos e da atuação dos deputados federais. No entanto, essa visibilidade nem sempre se traduz em clareza.

Isso gera um novo paradoxo: embora o volume de informação disponível seja o maior da história, encontrar a _verdade_ sobre a atuação parlamentar tornou-se uma tarefa mais difícil. O cidadão vê-se preso entre dois extremos:

1. **Dados Oficiais:** Ricos e precisos, mas apresentados de forma complexa, fragmentada e em jargão técnico nos portais governamentais.
2. **Narrativas de Redes Sociais:** De fácil consumo e alto poder de engajamento, mas frequentemente repletas de desinformação, gráficos enganosos e estatísticas falsas que acabam ofuscando os fatos.    

Este projeto nasce da necessidade de preencher essa lacuna. Nosso objetivo não é apenas "mostrar os dados", mas sim _competir_ com a desinformação, transformando dados públicos brutos em conhecimento acessível, visualmente claro e fácil de compartilhar.
### **2. Objetivo do Projeto**
Desenvolver uma plataforma web que atue como um **antídoto à desinformação**, quebrando a barreira de complexidade dos dados oficiais.

O objetivo é reequilibrar o debate público ao traduzir os dados brutos da Câmara dos Deputados em um formato acessível, intuitivo e visualmente claro. A plataforma permitirá que qualquer cidadão possa fiscalizar, entender e formar opinião sobre a atuação de seus representantes com base em **fatos verificados**.

### **3. Público-Alvo**
Para combater a desinformação de forma eficaz, o projeto foca em dois públicos estratégicos:

- **O Cidadão Fiscalizador:** Pessoas com interesse em política, mas que hoje se sentem frustradas com o volume de narrativas conflitantes e _fake news_. Elas buscam uma fonte  confiável e de fácil digestão para verificar fatos, acompanhar votações-chave e entender os gastos parlamentares, sem a necessidade de conhecimento técnico em análise de dados.
    
- **Os Multiplicadores de Informação:** Jornalistas e criadores de conteúdo digital. Eles necessitam de dados já consolidados, gráficos  e visualizações fáceis de exportar para agilizar seu trabalho de apuração, embasar reportagens, análises e publicações, enriquecendo o debate público com fatos verificados em larga escala.


---

![](../attachments/Pasted%20image%2020251209081402.png)

## **Definição de Telas e Funcionalidades

### **1. Tela Inicial**

- **Cabeçalho Global:** Logo, Menu de Navegação (Deputados, Partidos, Comparador, Match, Sobre) e Barra de Busca Geral (pesquisa por nome de deputado, partido ou tema).
    
- **Card "Sessão de Hoje":** Widget em destaque informando se há sessão no Plenário, qual a pauta principal do dia e link incorporado para a transmissão ao vivo da TV Câmara.
    
- **Destaques de Notícias:** Feed curado de atualizações relevantes sobre votações e tramitações.
![](../attachments/Pasted%20image%2020251209075113.png)
### **2. Tela do Deputado**

- **Cabeçalho do Perfil:** Foto oficial, Nome Parlamentar, Partido, Estado (UF), links para redes sociais e botões de ação ("Comparar", "Copiar Link").
    
- **Painel de Desempenho (KPIs):**
    - **Presença:** Gráfico de rosca.        
    - **Produção:** Contagem de projetos apresentados vs. aprovados.
        
- **Seção Financeira:**
	- Gráfico mostranod os gastos parlamentares por tipo (viagem, divulgação, abastecimento e etc.) e a comparação com a media de gastos dos parlmantares. Gráfico de barras lado a lado horizontalmente
        
- **Seção de Votações:** Lista filtrada das votações de alto impacto (sim/não/abstenção) com link para o "Modo Resumo".

- Ultimas noticias relacionadas a esse deputado

![](../attachments/Pasted%20image%2020251209075618.png)
### **3. Tela de Partidos

- **Cabeçalho da Sigla:** Logo, Nome, Número Eleitoral e tamanho da bancada atual.
    
- **Ranking Interno (Gamificação da Bancada):**
    - Deputado com maior uso da cota.
    - Deputado com menor uso da cota.
    - Deputado que mais vota contra a orientação do partido.
    
- Ultimas noticias relacionadas a esse partido

- Deputados asociados.

![](../attachments/Pasted%20image%2020251209080053.png)
### **4. Tela de Comparação

**Objetivo:** Permitir a análise lado a lado para decisão de voto ou fiscalização comparativa.

- **Seletor de Entidades:** Campos de busca para selecionar "Deputado A" vs. "Deputado B" (ou Deputado vs. Média do Estado).
    
- **Quadro Comparativo:** Tabela visual confrontando:
    - Presença em Plenário
    - Gasto total acumulado no ano.
    - Alinhamento com o Governo (%).
    - Posicionamento em votações chaves.
    
- Gastos por gategoria, comparação

- Posicionamento em algumas votaçoes importantes
        
- **Gerador de Card de Batalha:** Botão para exportar a comparação como imagem (PNG) otimizada para redes sociais (Stories/Feed).
![](../attachments/Pasted%20image%2020251209080515.png)
### **5. Tela "Match Legislativo"

**Objetivo:** Quebrar viés de confirmação e conectar o cidadão ao representante baseado em ideias, não em nomes.

- **Fluxo do Quiz:** Apresentação sequencial de 5 votações polêmicas recentes (sem revelar autores ou partidos).
    
- **Interação:** O usuário vota "A Favor", "Contra" ou "Indiferente".
    
- **Resultado:** O sistema cruza as respostas do usuário com a base de dados e exibe:

![](../attachments/Pasted%20image%2020251209080835.png)

### **6. Tela de Detalhes da Proposição**

- **Cabeçalho do Projeto:** Título oficial em destaque (ex: PL 2630/2020), Autor principal (com link para o perfil) e Data de apresentação.     
    
- **"O Que Muda na Minha Vida?" (IA):** Este é o coração da tela. Um box em destaque que utiliza o **Modo Resumo** para explicar o impacto prático da lei, substituindo a ementa técnica.     - _Exemplo:_ Em vez de "Altera a lei 12.3...", exibe: _"Este projeto proíbe o uso de celulares em salas de aula de escolas públicas e privadas."_     
    
- **Timeline Visual (Rastreador de Tramitação):** Uma barra de progresso horizontal (estilo status de pedido de app de entrega) mostrando visualmente onde o projeto está travado ou andando:     - _Etapas:_ Apresentação ➔ Comissões ➔ Plenário ➔ Senado ➔ Sanção Presidencial.     
    
- **Enquete Cidadã:** Um widget de engajamento perguntando: _"Você apoiaria esse projeto?"_ (Sim / Não). Exibe a porcentagem da opinião dos usuários da plataforma em tempo real.     
    
- **Documentos Originais:** Para o perfil "Multiplicador/Jornalista", um link discreto para baixar o PDF original do projeto e ver o histórico técnico completo.

- Se ja votado, uma lista exportavel com os votos de cada deputado.

![](../attachments/Pasted%20image%2020251209081236.png)