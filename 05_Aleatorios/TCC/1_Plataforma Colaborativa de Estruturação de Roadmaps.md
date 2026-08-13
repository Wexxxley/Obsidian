

---
### 1. Problema Central

Na contemporaneidade, a democratização digital permite o acesso a conteúdos educacionais sobre praticamente qualquer área do saber. Todavia, essa disponibilidade é acompanhada pelo fenômeno da fragmentação, no qual os recursos didáticos se apresentam dispersos em múltiplas plataformas e desprovidos de uma estrutura pedagógica. Em vez de o estudante se concentrar na aprendizagem, o indivíduo gasta sua energia na curadoria e na organização dos materiais e, mesmo assim, encontra lacunas. 

Este cenário é particularmente prejudicial para indivíduos autodidatas e estudantes que operam sem o suporte direto de tutores ou instituições de ensino.  Além disso, as trilhas de aprendizado estáticas sofrem de obsolescência precoce. A ferramenta precisa existir para fornecer uma **forma humanizada de organizar o conteúdo infinito**. A curadoria humana adiciona o contexto pedagógico e a validação qualitativa que algoritmos de busca genéricos não possuem. 
### 2. Objetivo Geral

Desenvolver uma plataforma colaborativa para a criação, evolução e curadoria de roadmaps educacionais, utilizando o desenvolvimento do sistema como um estudo de caso.

A plataforma não iria atuar como curadora, mas forneceria infraestrutura para que a comunidade realizasse a auto-curadoria.
- **Mantenedor**: Criador original ou responsável pelo roadmap "oficial". Define a filosofia pedagógica, revisa sugestões e garante a coesão da trilha.
- **Colaborador**: Qualquer usuário que identifique melhorias (links, novos conteúdos) poderia sugerir uma mudança.
### 3. Abordagem Metodológica e Arquitetural

**EspecificaçãUsing the Open Source Collaborative Model for Digital Educational
Contento de Requisitos**: 
- Os requisitos funcionais detalharão as regras de negócio intrínsecas à plataforma, como o fluxo de submissão de sugestões, a mecânica de revisão e aprovação pelos mantenedores, e o sistema de controle de acesso. 

**Modelagem de Dados e Estruturas em Grafos**: Uma etapa central da abordagem será a definição técnica da persistência dos _roadmaps_. Como as trilhas de aprendizado exigem a definição de pré-requisitos não lineares, os dados serão representados e estruturados como Grafos Direcionados Acíclicos (DAGs). O trabalho documentará a análise técnica entre diferentes paradigmas de banco de dados para armazenar essas hierarquias. 

**Versionamento, sincronização e Diferenciação**: Devido à alta complexidade computacional envolvida no gerenciamento de alterações concorrentes, este tópico será tratado como um módulo de estudo aprofundado isolado. A pesquisa investigará três pilares:
1. isolamento de estado (garantindo que as propostas de edição existam sem impactar a trilha oficial)
2. cálculo de diferenciação (a identificação algorítmica exata de quais nós e dependências foram inseridos, alterados ou removidos)
3. mecanismos de resolução de conflitos e mesclagem.

---
### 4. O que vai poder ser feito na plataforma
#### 4.1Criação e Modificação Direta do Roadmap

- **Foco Teórico Necessário:** Modelagem de Grafos em Bancos de Dados.    
- **O que estudar:** Como as trilhas educacionais possuem pré-requisitos, elas formam Grafos Direcionados Acíclicos (DAGs). O seu referencial teórico deverá focar nos padrões de persistência dessas estruturas. O estudo deve contemplar padrões estruturais em bancos de dados relacionais, como a Lista de Adjacência (_Adjacency List_), o Caminho Materializado (_Materialized Path_) e a Tabela de Fechamento (_Closure Table_). O objetivo é fundamentar qual desses padrões oferece a melhor performance para leitura e modificação direta da trilha.
#### 4.2 Sugestões de Alteração (O Modelo de Pull Request)

O sistema permitirá que usuários sugiram modificações em roadmaps públicos, cabendo ao mantenedor a aprovação ou rejeição da alteração estrutural.
- **Foco Teórico Necessário:** Isolamento de Estado e Algoritmos de Diferenciação.
- **O que estudar:** Primeiramente, é necessário pesquisar como isolar a sugestão do usuário para que ela não altere o roadmap original em produção. Isso exige o estudo de armazenamento de deltas (gravar apenas a diferença) versus armazenamento de cópias. Em segundo lugar, o estudo matemático do cálculo de diferenciação de árvores (_Tree Edit Distance - TED_). O referencial teórico deverá abordar o Algoritmo de Zhang-Shasha ou variações modernas para explicar formalmente como o sistema identificará e exibirá ao mantenedor quais tópicos o usuário inseriu, removeu ou alterou.
#### 4.3 Cópia de Roadmaps Públicos (O Modelo de Fork)

Usuários poderão copiar um roadmap público autorizado e assumir a manutenção dessa nova entidade independente.
- **Foco Teórico Necessário:** Estratégias de Replicação de Dados.
- **O que estudar:** O desafio computacional aqui é a eficiência de armazenamento. Se um roadmap possui centenas de tópicos e milhares de usuários realizarem a cópia, duplicar todos os registros de forma profunda (_Deep Copy_) causará um consumo massivo de armazenamento. Você deve estudar o princípio arquitetural do _Copy-on-Write_ (CoW), um conceito de otimização onde o sistema compartilha as referências aos dados originais e cria novos registros físicos apenas no momento em que o novo mantenedor efetua uma modificação na sua cópia.
#### 4.4 Colaboração Simultânea de Múltiplos Mantenedores

O mantenedor original poderá delegar permissões para que colaboradores editem diretamente o roadmap em conjunto, introduzindo complexidades de concorrência.
- **Foco Teórico Necessário:** Controle de Concorrência e Sincronização Distribuída.
- **O que estudar:** Este é o ponto que exige o estudo de Tipos de Dados Replicados Livres de Conflitos (CRDTs) e Transformação Operacional (OT). Como múltiplos usuários possuem permissão de escrita direta, o sistema precisará processar edições concorrentes. O estudo dos CRDTs baseados em estado fornecerá a base formal para garantir a comutatividade das operações, assegurando que, independentemente da ordem em que o servidor receba as requisições de alteração dos diferentes mantenedores, o roadmap final não entrará em estado de inconsistência. Adicionalmente, o estudo do Controle de Concorrência Otimista (MVCC) justificará o funcionamento das transações na camada do banco de dados.

Um nó poderia apontar para outro roadmap? um roadmap de roadmaps?

---
### **5. Tópicos a serem estudados**

**Modelagem de Grafos em Bancos de Dados**
Você deve estudar como representar essas estruturas hierárquicas e não lineares. Pesquise sobre os seguintes padrões:
- **Em Bancos Relacionais:** Estude os padrões _Adjacency List_ (Lista de Adjacência, onde cada registro aponta para o seu nó pai/filho direto), _Materialized Path_ (Caminho Materializado, que armazena a rota completa até o nó em uma única coluna) e _Closure Table_ (Tabela de Fechamento, que armazena todos os caminhos possíveis entre os nós, facilitando consultas profundas).
- **Em Bancos NoSQL (como MongoDB):** Estude a modelagem orientada a documentos aninhados e padrões de referenciamento de documentos para representar árvores e grafos.
**Controle de Concorrência**
Como o sistema é colaborativo, múltiplos usuários podem tentar alterar o mesmo _roadmap_ simultaneamente. É necessário estudar como os bancos de dados lidam com essas transações.
- **Optimistic Locking (Bloqueio Otimista):** Uma abordagem que permite múltiplas leituras e escritas simultâneas, validando a integridade dos dados apenas no momento da consolidação (geralmente utilizando uma coluna de versão no registro).
- **Pessimistic Locking (Bloqueio Pessimista):** Uma abordagem que bloqueia o registro no banco de dados assim que um usuário inicia uma alteração, impedindo que outros modifiquem o dado até a conclusão da transação.

**Design de APIs para Estruturas Complexas**
Você precisará justificar como o cliente requisitará a árvore de estudos.
- **Problemas de Over-fetching e Under-fetching:** Estude o impacto de requisições RESTful tradicionais, onde uma chamada pode trazer dados em excesso ou exigir múltiplas requisições em cadeia para montar o grafo completo.

**Event Sourcing (Fonte de Eventos)**
Trata-se de um padrão arquitetural onde o estado atual de um sistema não é armazenado diretamente. Em vez disso, armazena-se uma sequência cronológica de eventos (por exemplo, "Nó A criado", "Dependência B vinculada ao Nó A", "Nó C removido").
- **Relevância para o TCC:** Estudar esse padrão ajuda a entender como reconstruir qualquer versão passada de um _roadmap_ processando sequencialmente os eventos armazenados, facilitando auditorias e reversões de edições.

**Estruturas Internas do Git (Merkle Trees e DAGs)**
Para projetar um sistema que aceita sugestões, aprovações e controle de versão, é fundamental estudar a teoria matemática por trás das ferramentas já consolidadas.
- **Merkle Trees (Árvores de Hash):** Estruturas de dados onde cada nó não folha recebe um _hash_ criptográfico derivado dos seus nós filhos. Isso permite verificar a integridade e identificar alterações em grandes volumes de dados de forma extremamente rápida. O Git utiliza este conceito.

**Isolamento de Estado (Branching em Dados)**
Você deve pesquisar como replicar os dados de um _roadmap_ para que um colaborador faça edições sem corromper a versão original em produção.
- **Copy-on-Write (CoW):** Uma técnica de otimização de recursos onde o sistema não duplica a trilha de aprendizado inteira ao criar uma versão de rascunho. O sistema compartilha os dados originais e cria novos registros apenas para os nós específicos que foram alterados pela sugestão do colaborador.

**Algoritmos de Diferenciação em Grafos (Graph Diffing)**
A teoria sobre como identificar computacionalmente a diferença exata entre duas estruturas de dados não lineares.
- **Relevância para o TCC:** O sistema precisará comparar o grafo original do mantenedor e o grafo modificado pelo colaborador para exibir exatamente quais tópicos foram adicionados, movidos ou excluídos, antes da aprovação final.


---

FLUXO DE INTERAÇÃO DO USER.
MOTIVAÇÕES. distinção entre personagens, autor, colaborador
PQ ESSA FERRAMENTA PRECISA EXISTIR? FORMA HUMANIZADA DE ORGANIZAR CONTEUDO INFINITO. FLUXO DE DADOS VIÁVEL.
INTERFACE MÍNIMA DO USER.
A PROPOSTA/CAÇAR SITES/PROPOSTAS SEMELHANTES/IDEIAS SEMELHANTES.
PROPOSTA COLABORATIVO PARA CONSTRUIR ALGO, COM OAS PESSAOS INTERAGEM.
TabNews - conceito de economia interna. nao.
INSPIRADO NO GIT ?
SUGESTOES DE IA ONDE TAL CONTEUDO ENTRAR?
COM A WIKIPEDIA CONTROLA AS COLABORAÇOES? 
E SE PESSOAS ALEATORIAMENTE ESCREVESEM ALGO? modelos de validação.. VERIFICAÇÃO DE INFORMAÇÃO VÁLIDA. 