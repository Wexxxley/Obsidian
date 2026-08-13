

---



**1. INTRODUÇÃO** O desenvolvimento baseado em pull é um paradigma emergente para o desenvolvimento de software distribuído. À medida que mais desenvolvedores valorizam o desenvolvimento isolado e a criação de ramificações (_branching_), mais projetos, tanto de código fechado quanto, especialmente, de código aberto, estão sendo migrados para sites de hospedagem de código como Github e Bitbucket, que fornecem suporte para o desenvolvimento baseado em pull. Uma característica única de tais sites é que eles permitem que qualquer usuário clone qualquer repositório público. O clone cria um projeto público que pertence ao usuário que o clonou, de forma que o usuário possa modificar o repositório sem fazer parte da equipe de desenvolvimento. Além disso, tais sites automatizam a contribuição seletiva de _commits_ do clone para a origem através de _pull requests_.

Os _pull requests_ como um modelo de desenvolvimento distribuído em geral, e conforme implementados pelo Github em particular, formam um novo método de colaboração no desenvolvimento de software distribuído. A novidade reside na dissociação do esforço de desenvolvimento da decisão de incorporar os resultados desse desenvolvimento na base de código. Ao separar as preocupações de construção de artefatos e integração de alterações, o trabalho é claramente distribuído entre uma equipe de contribuidores que submete alterações (muitas vezes ocasionais) para serem consideradas para mesclagem, e uma equipe principal que supervisiona o processo de mesclagem, fornecendo feedback, conduzindo testes, solicitando mudanças e, finalmente, aceitando as contribuições.

Trabalhos anteriores identificaram os processos de colaboração no desenvolvimento distribuído por meio da submissão e aceitação de _patches_. Existem muitas semelhanças com a forma como os _pull requests_ funcionam; por exemplo, estruturas de equipe de trabalho semelhantes emergem, uma vez que tipicamente os _pull requests_ passam por um processo de avaliação. O que os _pull requests_ oferecem adicionalmente é a automação de processos e a centralização de informações. Com _pull requests_, o código não precisa sair do sistema de controle de revisão e, portanto, pode ser versionado entre repositórios, enquanto as informações de autoria são mantidas sem esforço. A comunicação sobre a alteração é específica ao contexto, enraizada em um único _pull request_. Além disso, o mecanismo de revisão incorporado pelo Github tem o efeito adicional de melhorar a conscientização (_awareness_); os desenvolvedores principais podem acessar de forma eficiente todas as informações relacionadas a um _pull request_ e solicitar opiniões da comunidade ("_crowd-source_") sobre a decisão de mesclagem.

Um fluxo de trabalho de desenvolvimento distribuído é eficaz se os _pull requests_ forem eventualmente aceitos, e é eficiente se o tempo que isso leva for o mais curto possível. Avançar nossa compreensão sobre a eficácia e eficiência no processamento de _pull requests_ é de interesse direto para contribuidores e desenvolvedores igualmente. O objetivo deste trabalho é obter um entendimento profundo sobre o uso de _pull requests_ e analisar os fatores que afetam a eficiência do modelo de desenvolvimento de software baseado em pull. Especificamente, as questões que estamos tentando responder são:

- **RQ1** Quão popular é o modelo de desenvolvimento baseado em pull?
        
- **RQ2** Quais são as características do ciclo de vida dos _pull requests_?
    
- **RQ3** Quais fatores afetam a decisão e o tempo necessário para mesclar um _pull request_?
    
- **RQ4** Por que alguns _pull requests_ não são mesclados?
    

Nosso estudo é baseado em dados da forja de desenvolvimento colaborativo Github, conforme disponibilizados pelo nosso projeto GHTorrent. Usando esses dados, primeiro exploramos o uso de quase 2 milhões de _pull requests_ em todos os projetos no Github. Em seguida, examinamos 291 projetos cuidadosamente selecionados em Ruby, Python, Java e Scala (um total de 166.884 _pull requests_) e identificamos, usando análise qualitativa e quantitativa, os fatores que afetam o tempo de vida, a mesclagem e a rejeição de _pull requests_.

  

**2. CONTEXTO (BACKGROUND)** Desde o surgimento das primeiras implementações de código aberto em 2001, os sistemas de controle de versão distribuídos (DVCS), notadamente o Git, revolucionaram a forma como o desenvolvimento de software distribuído é conduzido. Impulsionados por necessidades pragmáticas, a maioria dos DVCSs foi projetada do zero para funcionar como sistemas avançados de gerenciamento de _patches_, em vez de sistemas de arquivos versionados (o paradigma de controle de versão dominante na época). Na maioria dos DVCSs, um arquivo é um conjunto ordenado de mudanças, cuja aplicação serial leva ao estado atual. As alterações são marcadas por identificadores globalmente exclusivos, que podem ser usados para rastrear o conteúdo do _commit_ entre repositórios. Ao integrar mudanças, os conjuntos de alterações podem originar-se de um sistema de arquivos local ou de um host remoto; ferramentas facilitam a aquisição e aplicação desses conjuntos em um espelho local. A natureza distribuída dos DVCSs permite um modelo de desenvolvimento baseado em pull, onde as mudanças são oferecidas ao repositório do projeto por meio de uma rede de bifurcações (_forks_) do projeto; cabe ao proprietário do repositório aceitar ou rejeitar os _pull requests_ recebidos.

O propósito do desenvolvimento distribuído é permitir que um contribuidor potencial submeta um conjunto de alterações a um projeto de software gerenciado por uma equipe principal. Os modelos de desenvolvimento oferecidos pelos DVCSs são um superconjunto daqueles encontrados em ambientes de controle de versão centralizados. Em relação ao recebimento e processamento de contribuições externas, as seguintes estratégias podem ser empregadas com DVCS:

- **Repositório compartilhado.** A equipe principal compartilha o repositório do projeto, com permissões de leitura e escrita, com os contribuidores. Para trabalhar, os contribuidores o clonam localmente, modificam seu conteúdo, potencialmente introduzindo novas ramificações, e enviam (_push_) suas alterações de volta ao repositório central. Para lidar com múltiplas versões e múltiplos desenvolvedores, projetos maiores geralmente adotam um modelo de ramificação (_branching model_), ou seja, uma maneira organizada de inspecionar e testar contribuições antes que elas sejam mescladas no ramo de desenvolvimento principal.
    
      
    
- **Pull requests.** O repositório principal do projeto não é compartilhado com contribuidores potenciais; em vez disso, os contribuidores bifurcam (_fork_ / clonam) o repositório e fazem suas alterações independentes uns dos outros. Quando um conjunto de alterações está pronto para ser submetido ao repositório principal, eles criam um _pull request_, que especifica um ramo local para ser mesclado com um ramo no repositório principal. Um membro da equipe principal do projeto é então responsável por inspecionar as alterações e puxá-las (_pull_) para o ramo mestre do projeto. Se as mudanças forem consideradas insatisfatórias, mais mudanças podem ser solicitadas; nesse caso, os contribuidores precisam atualizar seus ramos locais com novos _commits_. Além disso, como os _pull requests_ especificam apenas ramos dos quais certos _commits_ podem ser puxados, não há nada que proíba seu uso na abordagem de repositório compartilhado (_pull requests_ entre ramificações).
    
      
    

**Pull Requests no Github.** O Github suporta todos os tipos de desenvolvimento distribuído descritos acima; no entanto, os _pull requests_ recebem um tratamento especial. O site é ajustado para permitir a fácil bifurcação de projetos por contribuidores, ao mesmo tempo em que facilita a geração de _pull requests_ por meio da comparação automática de ramificações do projeto. O modelo de _pull request_ do Github segue o padrão genérico apresentado acima; além disso, ele fornece ferramentas para discussões contextuais e revisões de código _in-line_.

  

Um _pull request_ no Github contém uma ramificação (local ou em outro repositório) a partir da qual um membro da equipe principal deve puxar os _commits_. O Github descobre automaticamente os _commits_ a serem mesclados e os apresenta no _pull request_. Por padrão, os _pull requests_ são enviados ao repositório base ("_upstream_") para inspeção. A inspeção é uma revisão de código dos _commits_ submetidos ou uma discussão sobre os recursos introduzidos. Qualquer usuário do Github pode participar de ambos os tipos de inspeção. Como resultado da inspeção, os _pull requests_ podem ser atualizados com novos _commits_ ou fechados como redundantes, desinteressantes ou duplicados. Em caso de atualização, o contribuidor cria novos _commits_ no repositório bifurcado, enquanto o Github atualiza automaticamente os _commits_ exibidos. A inspeção do código pode então ser repetida.

  

Quando o processo de inspeção termina e as mudanças são consideradas satisfatórias, o _pull request_ pode ser mesclado. Um _pull request_ só pode ser mesclado por membros da equipe principal. A versatilidade do Git permite que _pull requests_ sejam mesclados de três maneiras:

  

1. **Através das facilidades do Github.** O Github verifica automaticamente se um _pull request_ pode ser mesclado sem conflitos no repositório base. Quando uma mesclagem é solicitada, o Github aplica automaticamente os _commits_ e registra o evento de mesclagem. Toda a autoria e histórico são mantidos.
    
      
    
2. **Usando o merge do Git.** Quando um _pull request_ não pode ser aplicado de forma limpa ou quando as políticas do projeto não permitem a mesclagem automática, utilitários do Git podem ser usados através de:
    
      
    - **Branch merging:** A ramificação no repositório bifurcado é mesclada a uma ramificação no repositório base. Histórico e autoria são mantidos, mas o Github não consegue registrar o evento.
        
          
        
    - **Cherry-picking:** O mesclador seleciona _commits_ específicos do ramo remoto e os aplica ao ramo base. O identificador do _commit_ muda, então o histórico exato não é mantido, mas a autoria é preservada. Uma técnica complementar é o **commit squashing**: vários _commits_ são combinados em um único antes de serem mesclados, alterando o autor original no registro.
        
          
        
3. **Aplicando o patch (Committing the patch).** O mesclador cria uma diferença textual e a aplica ao ramo principal. Histórico e autoria são perdidos.
    
      
    

Conflitos de mesclagem acontecem quando as alterações em um _pull request_ interferem em novas alterações feitas no ramo principal do projeto. O Github detecta esses conflitos automaticamente. A etiqueta exige que o próprio contribuidor resolva os conflitos puxando novos _commits_ da base, alterando o código localmente e atualizando o _pull request_.

  

_Issues_ e _pull requests_ funcionam de forma paralela no Github; para cada _pull request_, uma _issue_ (tarefa/problema) é aberta automaticamente. Essa dualidade permite que a equipe gerencie _pull requests_ usando os mesmos recursos do rastreador de problemas. Além disso, padrões em mensagens de _commit_ podem fechar problemas automaticamente após a mesclagem. A natureza aberta permite seu uso como ferramentas para discussão de design ou acompanhamento de marcos (milestones) de lançamento.

  

**3. DESIGN DA PESQUISA** O foco principal deste estudo é entender e explicar como os _pull requests_ são usados para permitir a colaboração. Para responder às nossas questões de pesquisa, usamos uma abordagem de métodos mistos sequenciais, ou seja, um procedimento que coleta, analisa e integra dados quantitativos e qualitativos para obter uma melhor compreensão do problema. Abaixo, apresentamos como abordamos cada questão de pesquisa.

  

- **RQ1**: Para avaliar a popularidade do modelo, fornecemos estatísticas descritivas sobre o uso de _pull requests_ no Github. Investigamos quantos projetos o utilizam, quantos são repositórios originais (em oposição a _forks_) e a relação com as ferramentas de rastreamento de _issues_. (Resultados na Seção 5).
    
      
    
- **RQ2 e RQ3**: Identificar as características do ciclo de vida e determinar os fatores que as afetam requer um conjunto de dados com histórico suficiente. Extraímos características baseadas na literatura e refinamos isso via análise de correlação cruzada para obter variáveis preditivas. Respondemos a RQ2 estatisticamente e usamos aprendizado de máquina (como algoritmos _Random Forests_, Regressão Logística e _Naïve Bayes_) para identificar os fatores dominantes (RQ3) que definem se e quão rápido a mesclagem ocorre.
    
      
    
- **RQ4**: Para examinar por que alguns _pull requests_ não são mesclados, analisamos qualitativamente um conjunto de _pull requests_ não mesclados usando teoria fundamentada (_open coding_). A primeira avaliação identificou os motivos de rejeição em categorias. Todos os autores validaram esses códigos em novas amostras, cruzaram os resultados e, finalmente, aplicaram os parâmetros finais a um total de 350 casos escolhidos aleatoriamente.

**4. DADOS** **4.1 Dados do Github** Os autores utilizaram dados do Github disponibilizados pelo projeto GHTorrent, que atua como um espelho offline da API do Github. Esse banco de dados coleta eventos em tempo real, como criações de _pull requests_ e problemas (_issues_), abrangendo mais de 1,9 milhão de _pull requests_ e centenas de milhares de projetos desde fevereiro de 2012 até agosto de 2013.

  

**4.2 Amostra de Projetos de Pull Request** Para fins práticos e para evitar analisar projetos superficiais ("de brinquedo"), os pesquisadores selecionaram repositórios que registraram mais de 200 _pull requests_. Eles aplicaram critérios rigorosos de exclusão: os projetos deveriam ter testes (limitando a seleção aos ecossistemas Ruby, Python, Java e Scala), possuir ao menos um _commit_ originado de _pull request_ para provar abertura a contribuições externas e focar em frameworks ou aplicações reais. O conjunto final foi de 291 projetos e 166.884 _pull requests_. Os autores também empregaram regras heurísticas para detectar quando um código era mesclado fora da plataforma oficial do Github e extraíram características em três categorias: características do _pull request_ (tamanho, linhas modificadas), características do projeto (tamanho da equipe) e características do desenvolvedor (taxa de sucesso prévia).

  

**4.3 Dados Qualitativos** Para entender os motivos das rejeições, foi conduzida uma análise qualitativa em uma amostra de 350 _pull requests_ selecionados aleatoriamente. Os autores validaram cruzadamente as categorias de rejeição antes de extraírem as conclusões finais.

  

**5. POPULARIDADE DO DESENVOLVIMENTO BASEADO EM PULL (RQ1)** Apesar do Github possuir milhões de repositórios, menos da metade (45%) são repositórios originais, sendo o restante bifurcações (_forks_). Observou-se que apenas 14% dos repositórios ativos utilizam o modelo de _pull requests_, número quase equivalente aos projetos que preferem a abordagem de "repositório compartilhado". Embora o uso em números absolutos esteja crescendo, mais de 73% das solicitações abertas em 2013 foram mescladas com sucesso. Conclui-se que o modelo é altamente eficaz para atrair contribuições externas, com revisões e discussões originadas majoritariamente pela própria comunidade.

  

**6. CICLO DE VIDA DO PULL REQUEST (RQ2)** A análise revelou que 84,73% dos _pull requests_ são aceitos e mesclados. O tempo de processamento é extremamente rápido: 80% são resolvidos em cerca de 3,7 dias e 30% em menos de uma hora. Os pesquisadores não encontraram diferença estatística significativa no tratamento dado aos membros da equipe principal em comparação aos contribuidores externos, indicando um processo igualitário. A grande maioria dos pacotes de código submetidos é pequena, contendo menos de 20 linhas de alteração. A presença de código de teste anexo não acelerou nem aumentou as chances de aprovação, enquanto o rigor de revisões explícitas de código atrasou ligeiramente o tempo de aprovação.

  

**7. MESCLAGEM E TEMPO DE MESCLAGEM (RQ3)** Utilizando algoritmos de aprendizado de máquina (como o _Random Forest_), os autores buscaram prever o sucesso e a velocidade de uma contribuição. A decisão final de aceitar um _pull request_ é dominada por um fator principal: se o pacote de código modifica uma área do sistema que está atualmente sob desenvolvimento ativo. Por outro lado, a velocidade com que o pedido é aprovado não possui um único fator dominante, dependendo mais da reputação e histórico anterior do desenvolvedor no projeto, do tamanho geral do código-fonte e da cobertura de testes existente.

  

**8. PULL REQUESTS NÃO MESCLADOS (RQ4)** Ao analisar por que pedidos de mesclagem falham, identificou-se que apenas 13% são rejeitados por problemas técnicos (como implementação incorreta). A esmagadora maioria (53%) das recusas ocorre devido à natureza paralela do sistema: alterações concorrentes no código (27%), mudanças consideradas desinteressantes ou redundantes pela direção do projeto (16%) e falhas em seguir as convenções operacionais exigidas (10%). Isso sugere que o maior obstáculo para a colaboração é a falta de comunicação ou desalinhamento de objetivos, e não a habilidade técnica.

  

**9. DISCUSSÃO**

  

- **9.1 O Modelo de Desenvolvimento:** O estudo reforça que o modelo baseado em _pull requests_ democratiza o desenvolvimento de código aberto. Como os desenvolvedores casuais têm chances reais de aprovação sem depender de hierarquias, a taxa de sucesso (mais de 70%) supera antigos métodos baseados em listas de e-mail.
    
      
    
- **9.2 Implicações:** Os autores aconselham que os contribuidores foquem em modificar áreas "quentes" do código com pequenas atualizações. Para as equipes de gestão, investir em testes automatizados e regras de transparência ajuda a processar o volume de solicitações rapidamente.
    
      
    
- **9.3 Ameaças à Validade:** Os dados agruparam projetos de todos os tamanhos, o que pode ofuscar nuances operacionais de repositórios muito pequenos. A coleta também sofreu limitações naturais das heurísticas automatizadas de detecção de autoria.
    
      
    

**10. TRABALHOS RELACIONADOS** Esta seção posiciona a pesquisa dentro da literatura existente sobre Sistemas de Controle de Versão Distribuídos (DVCS). Os autores debatem semelhanças metodológicas com estudos passados sobre aprovação de correções (_patches_) no kernel do Linux e sistemas de revisão por pares em gigantes como Mozilla e Apache.

  

**11. CONCLUSÃO** O artigo sumariza que, embora represente uma fatia de 14% do mercado ativo da plataforma, o desenvolvimento baseado em pull é altamente veloz e igualitário. Problemas de rejeição estão profundamente mais enraizados na coordenação das tarefas distribuídas do que em gargalos técnicos.

  

**12. AGRADECIMENTOS** Os pesquisadores reconhecem o suporte de revisores anônimos e o financiamento estrutural por meio de projetos como o Marie Curie IEF e o TestRoots (NWO).

  

**13. REFERÊNCIAS** O documento encerra listando 32 referências acadêmicas utilizadas na formulação empírica do artigo, contendo livros clássicos sobre controle de versão e papers de engenharia de software extraídos de conferências proeminentes.