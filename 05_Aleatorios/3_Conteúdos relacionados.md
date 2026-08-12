


---

- **Roadmap.sh:** Possui roadmaps para desenvolvedores, porém a plataforma em si é estática para o usuário final. A colaboração acontece nos bastidores, através de repositórios no GitHub, o que exige conhecimento técnico avançado (Git) e afasta usuários comuns ou de outras áreas do conhecimento. O seu projeto inova ao trazer essa colaboração diretamente para uma interface de usuário visual e simplificada.
    
      
    
- **Wikipedia (O Modelo de Curadoria Aberta):** A Wikipedia é o principal exemplo de curadoria de conteúdo descentralizada. O modelo de controle baseia-se na transparência absoluta: todas as edições são registradas em um histórico imutável. Para evitar inserções aleatórias ou vandalismo, a plataforma utiliza um sistema de moderação reativa. O conteúdo é publicado imediatamente, mas a comunidade possui ferramentas de reversão rápida (_reverts_) para restaurar a página ao estado anterior em um único clique.
    
      
    
- **GitHub (O Modelo de Curadoria Fechada):** Diferente da Wikipedia, o GitHub adota um controle proativo. Através do conceito de _Pull Request_ (Solicitação de Alteração), as modificações propostas por terceiros ficam isoladas em um ambiente de aprovação. O código original permanece inalterado até que o mantenedor principal revise e autorize a mesclagem. Este é o modelo mais seguro para o seu escopo de roadmaps educacionais.
    
      
    

### 2. A Motivação e a Justificativa

A justificativa responde à pergunta do orientador: "Por que essa ferramenta precisa existir?".

  

O cenário atual da internet não sofre de escassez de informação, mas sim de excesso de ruído. Motores de busca e algoritmos de recomendação entregam conteúdos fragmentados. A ferramenta precisa existir para fornecer uma **forma humanizada de organizar o conteúdo infinito**.

  

A curadoria humana adiciona o contexto pedagógico e a validação qualitativa que algoritmos de busca genéricos não possuem. O objetivo da plataforma é estabelecer um **fluxo de dados viável**, transformando materiais didáticos dispersos (vídeos, artigos, documentações) em uma sequência lógica, progressiva e verificada por especialistas ou pela própria comunidade.

  

### 3. Distinção de Personagens e Papéis

O controle de qualidade e a verificação de informações válidas dependem de uma hierarquia clara de permissões. O escopo deve definir rigorosamente três atores principais:

  

- **Autor / Mantenedor Oficial:** É o criador original do _roadmap_. Este personagem detém o poder de veto. A responsabilidade do mantenedor é definir a linha pedagógica da trilha, revisar as propostas enviadas e garantir que a estrutura permaneça coesa, evitando que o _roadmap_ se transforme em um aglomerado de links sem sentido.
    
      
    
- **Colaborador:** Qualquer usuário autenticado no sistema. O colaborador consome o conteúdo, mas possui a permissão técnica para sugerir adições, correções de links quebrados ou remoção de tópicos obsoletos. A sua atuação é restrita à sugestão; nenhuma alteração proposta pelo colaborador afeta diretamente a versão oficial sem a aprovação do mantenedor.
    
      
    
- **Estudante / Consumidor Final:** Usuário que utiliza a plataforma puramente para navegação e consumo do conteúdo, guiando-se pelas trilhas já consolidadas, sem envolvimento no processo de edição.
    
      
    

### 4. Fluxo Mínimo de Interação do Usuário (User Flow)

Para definir a interface mínima e o fluxo de dados, o ciclo de vida de uma colaboração deve ser mapeado passo a passo.

  

1. **Descoberta e Consumo:** O estudante acessa a plataforma e busca um _roadmap_ público (por exemplo, "Matemática Discreta"). Ele visualiza a árvore de tópicos e inicia os estudos.
    
      
    
2. **Identificação de Lacuna:** Durante o estudo, o usuário percebe que um tópico específico está com um link desatualizado ou identifica um material mais didático na internet. O usuário decide atuar como Colaborador.
    
      
    
3. **Proposta de Alteração:** O colaborador aciona a interface de edição (isolada do original) e insere o novo link ou propõe um novo nó na árvore de dependências.
    
      
    
4. **Sugestão de IA (Conforme apontamento do orientador):** Neste momento da submissão, uma Inteligência Artificial pode processar o conteúdo do link sugerido e indicar automaticamente ao colaborador ou ao mantenedor a posição mais lógica para inserir aquele tópico dentro do grafo do _roadmap_, baseando-se na similaridade semântica do texto.
    
      
    
5. **Validação e Aprovação:** O Mantenedor Oficial recebe uma notificação. A interface exibe a diferença visual exata entre o _roadmap_ atual e a sugestão do colaborador. O mantenedor analisa a validade da informação e clica em aprovar.
    
      
    
6. **Consolidação:** O sistema mescla as informações e o _roadmap_ oficial passa a exibir o novo material, registrando o crédito ao colaborador.
    
      
    

### 5. Modelos de Validação de Informação

Para evitar que "pessoas aleatoriamente escrevam algo", o sistema rejeitará modelos de publicação direta. O controle de colaborações será estruturado com base nas seguintes regras de negócio de validação:

  

- **Validação Proativa (Isolamento de Estado):** Nenhuma modificação submetida por um colaborador altera os dados principais. O fluxo garante que todo novo conteúdo passe obrigatoriamente por um processo de curadoria humana por parte do mantenedor oficial antes da publicação.
    
      
    
- **Validação Automatizada de Recursos:** Antes mesmo do mantenedor revisar a sugestão, o sistema pode executar rotinas automatizadas básicas no _backend_, como verificar se as URLs sugeridas pelo colaborador respondem com códigos de sucesso (HTTP 200), bloqueando automaticamente a submissão de links quebrados ou endereços maliciosos.
    
      
    

Com este documento, você possui a fundamentação teórica e as regras de negócio bem definidas para apresentar ao orientador e obter a aprovação do escopo inicial.