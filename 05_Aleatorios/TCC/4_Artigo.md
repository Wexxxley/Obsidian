
---

**Utilizando o Modelo Colaborativo de Código Aberto para Conteúdo Educacional Digital**

  
**Resumo** O aprendizado auxiliado por computador tem visto recentemente uma adoção significativa entre os estudantes. Ferramentas automatizadas que oferecem cursos online, tutoria auxiliada por inteligência artificial, itens de prática, etc., foram desenvolvidas e estão disponíveis para uso. No outro lado do espectro, aos educadores é oferecida pouca melhoria para o processo de curadoria dos materiais educacionais que devem ser usados em sala de aula. Pior ainda, embora na maioria dos casos o currículo para uma área seja semelhante, diferentes educadores criam diferentes materiais de apoio, lições de casa, itens de prática e testes. A preparação para o que foi citado acima é significativa e o conteúdo educacional produzido é criado, usado e revisado por um pequeno número de pessoas. Neste artigo, propomos uma metodologia inovadora para usar o modelo colaborativo de código aberto para criar, usar e entregar conteúdo educacional de alta qualidade. O conteúdo educacional desenvolvido seguindo as diretrizes da nossa metodologia é fácil de usar, modificar e remixar. Os educadores que desejam usar o conteúdo podem facilmente selecionar os tópicos de interesse a partir de um conjunto proposto e todos os materiais educacionais, como materiais de leitura, tarefas, itens de prática e até mesmo itens de exame, serão gerados. Parte do conteúdo é disponibilizada aos alunos por meio de um site gerado, enquanto outras partes do conteúdo (como itens de exame ou soluções de tarefas) podem ficar ocultas. Além disso, todo esse conteúdo é público e pode ser usado por qualquer pessoa, incluindo alunos de todos os tipos (autodidatas ou seguindo um programa formal). Portanto, o conteúdo pode ser revisado e atualizado por vários educadores e alunos de forma igual. Usamos a metodologia proposta para criar materiais educacionais para vários cursos universitários e apresentamos o impacto do uso de tais materiais sob a perspectiva tanto do educador quanto do aluno.


**1. INTRODUÇÃO** Programas de computador educacionais têm sido usados com grande sucesso para estimular e aprofundar o processo de aprendizagem. Exemplos de tais ferramentas são: cursos online para a maioria das disciplinas de estudo (do nível iniciante ao especialista), sites que oferecem bancos de exercícios que são avaliados automaticamente, programas de tutoria que aproveitam as capacidades de inteligência artificial para fornecer incrementalmente explicações e exercícios para os alunos.

Embora essas ferramentas possam ser usadas até certo ponto individualmente pelos alunos, o ideal é que fossem integradas pelos educadores em seus métodos. No entanto, dada a vasta quantidade de ferramentas e recursos disponíveis na Internet, os educadores costumam gastar quantidades exorbitantes de tempo para pesquisar, selecionar, adaptar e fornecer materiais educacionais em vários formatos: slides, itens práticos, exames, trabalhos de casa, projetos, etc.

Para piorar a situação, cada educador faz a sua própria devida diligência para uma aula específica, duplicando assim o esforço de outros educadores da mesma área. Embora os materiais de apresentação, como os slides, possam ser adaptados às necessidades de cada um, outros conteúdos, como itens práticos e perguntas de exames, podem ser partilhados entre os educadores para facilitar a reutilização e a colaboração. Idealmente, os materiais de aprendizagem para cada área de estudo seriam armazenados em um local público, onde qualquer educador ou aluno pudesse acessar. Além disso, o conteúdo deve ser fácil de entender, navegar, selecionar, adaptar e publicar para os alunos. Neste caso, qualquer educador pode aceder ao conteúdo e utilizá-lo de acordo com as suas necessidades, minimizando assim o esforço de produção de materiais para as aulas. Como benefício adicional, o conteúdo seria usado por mais educadores e, portanto, poderia ser melhorado de forma colaborativa.

Para esse fim, neste artigo propomos uma metodologia nova para criar, usar e fazer curadoria de conteúdo educacional de alta qualidade, usando o modelo colaborativo de código aberto. Além disso, fornecemos um conjunto de ferramentas que podem ser usadas para criar conteúdo educacional ou para personalizá-lo e usá-lo diretamente. O conteúdo produzido por meio da nossa metodologia é disponibilizado ao público em geral, bastando ter ligação à Internet para o aceder. Todos os materiais educativos são facilmente modificáveis, uma vez que fornecemos todo o conteúdo num formato editável que pode ser utilizado para gerar conteúdos imutáveis (como ficheiros .pdf ou .png). Os educadores podem selecionar facilmente um subconjunto dos tópicos apresentados e as ferramentas que fornecemos irão gerir a implantação do conteúdo com todos os materiais necessários. Além disso, nos esforçamos para automatizar o máximo possível tarefas educacionais que exigem muito esforço, como: a avaliação de itens práticos, trabalhos e exames.

O benefício adicional de nossa abordagem é representado pelo fato de que o conteúdo pode ser compartilhado entre vários educadores, o que criará uma comunidade ao seu redor, incentivada a manter um alto padrão.

Aplicamos nossa metodologia no desenvolvimento de materiais educacionais para diversos cursos universitários de um programa de Ciência da Computação. Mostramos que o uso do modelo colaborativo para conteúdo educacional é benéfico não apenas para os educadores, mas também para os alunos. Em nosso caso específico, os alunos se beneficiaram por ter a avaliação automática da maioria de suas tarefas e por contribuir ativamente com o conteúdo educacional.

Em suma, as principais contribuições deste artigo são:
- Propomos uma metodologia nova para a criação, utilização e curadoria de conteúdo educacional de alta qualidade, utilizando o modelo colaborativo de código aberto.
- Propomos uma gama de ferramentas de código aberto que podem ser usadas para criar e usar conteúdo educacional de alta qualidade.
- Usamos nossa metodologia para criar conteúdo educacional para vários cursos universitários.
- Apresentamos o impacto tanto nos alunos quanto nos assistentes de ensino sobre o uso da metodologia proposta.
    

**2. VISÃO GERAL**
A metodologia proposta visa fornecer respostas a questões comuns relacionadas com conteúdos educativos, tais como:
- Como eu desenvolvo / crio um repositório de conteúdo educacional digital?
- Como eu uso (como educador) um repositório de conteúdo educacional digital numa implementação real (curso, treinamento)?
- Como eu contribuo para um repositório de conteúdo educacional digital?
- Como eu faço a curadoria / gerencio um repositório de conteúdo educacional digital?

Ao fornecer respostas a estas questões, a metodologia oferece diretrizes uniformes que são seguidas por diferentes tipos de conteúdos. Novos repositórios de conteúdo que sigam as mesmas diretrizes apresentarão uma visão confortável e familiar para desenvolvedores, usuários e mantenedores de conteúdo. Para tanto, a metodologia gira em torno de três conceitos-chave:
- **Aspectos do conteúdo:** São classes de ações relacionadas ao conteúdo digital no processo educacional.
- **Papéis:** São papéis das partes interessadas no processo educativo. Existe um mapeamento individual entre funções e aspectos do conteúdo.
- **Infraestrutura:** São componentes digitais que são utilizados em todo o processo educacional.

A infraestrutura digital serve de ponto comum para três funções e três aspectos de ensino. Cada um dos três aspectos de ensino e, portanto, cada uma das três funções, depende da infraestrutura e gera um tipo de saída a partir de um tipo de entrada. Estes três fluxos são detalhados a seguir:

1. **Os criadores de conteúdo (Content creators)** desenvolvem e organizam materiais de aprendizagem de alta qualidade que respeitam os 5 Rs dos recursos educacionais abertos: Reter, Reutilizar, Revisar, Remixar, Redistribuir. Eles utilizam ideias, conhecimentos e boas práticas como insumos para produzir repositórios de conteúdos como produtos. A infraestrutura utilizada consiste em ferramentas de código aberto para armazenamento, revisão e validação de conteúdos digitais.
2. **Os educadores (Educators)** configuram, implantam e entregam esses materiais aos alunos. Eles utilizam os repositórios de conteúdos como dados de entrada para produzir cursos digitais reais como resultados. A infraestrutura empregada consiste em mecanismos para formatar o conteúdo e automatizar fluxos de trabalho de ensino.    
3. **Os curadores de conteúdo (Content curators)** mantêm e gerenciam o conteúdo existente. Eles usam os repositórios de conteúdo e os cursos digitais como insumos para melhorar os repositórios e criar comunidades em torno desse conteúdo. A infraestrutura utilizada consiste nas mesmas ferramentas de armazenamento, revisão e validação de conteúdos, aliadas a ferramentas de comunicação e colaboração para incluir os educadores que utilizam os conteúdos.
    
Observe que uma pessoa pode preencher diversas funções. Por exemplo, alguém pode optar por preencher apenas a função de educador e usar o conteúdo existente. Na ausência de conteúdo, alguém pode assumir o papel de criador para desenvolvê-lo, de educador para ministrá-lo e de curador para manter a comunidade.

**3. CONTEXTO (BACKGROUND)** Os ambientes de aprendizagem baseados na Web cresceram significativamente em uso e popularidade nas últimas décadas. Algumas destas plataformas são abertas e de uso gratuito, outras são produtos comerciais. Estas plataformas digitais, que vão desde Sistemas de Gestão de Aprendizagem (LMS) abrangentes, como o Moodle e o Canvas, até plataformas de Cursos Online Abertos e Massivos (MOOCs), como o Coursera e o edX, oferecem experiências de aprendizagem diversas e personalizáveis.

  

Para aqueles que se concentram em habilidades técnicas, plataformas de codificação interativas como a Codecademy fornecem exercícios práticos de programação, enquanto plataformas como a DataCamp oferecem cursos em análise de dados. Existem também plataformas especializadas, como o Duolingo para o aprendizado de idiomas, e o tutor-web, um ambiente de código aberto projetado para ensinar matemática e estatística. Muitas dessas plataformas oferecem recursos que vão além da simples entrega de conteúdo, como avaliações interativas, fóruns de discussão, ferramentas de revisão por pares e mecanismos para os instrutores fornecerem feedback (um elemento-chave na aprendizagem dos alunos). Diversos estudos demonstraram evidências firmes de que inovações concebidas para fortalecer o feedback frequente produzem ganhos de aprendizagem substanciais. Fornecer esse feedback de qualidade pode ser demorado para os educadores, mas ao usar essas ferramentas, os alunos podem obter um retorno sem exigir a correção manual pelos professores.

  

Não há dúvida de que os ambientes baseados na Web aumentaram a acessibilidade à aprendizagem, quebrando barreiras tradicionais. No entanto, do ponto de vista do professor, existe frequentemente uma limitação nestas plataformas: elas não são facilmente abertas a contribuições, o que significa que o educador não tem a possibilidade de selecionar subconjuntos de tópicos ou organizar cursos inteiros adaptados exclusivamente às necessidades dos seus alunos.

  

Para resolver estes problemas, foram feitas tentativas de utilizar sistemas de controle de versão, como o Github, para armazenar recursos e partilhá-los. O GitHub é uma boa escolha, pois promove a colaboração e facilita o trabalho conjunto, permitindo rastrear alterações e oferecer recursos que podem ser acessados e melhorados por todos, até mesmo pelos alunos, além de oferecer hospedagem gratuita por meio do GitHub Pages.

  

Embora existam múltiplos repositórios de cursos, cada um implementa a sua própria estrutura e opções de implantação. Como não há um padrão, é difícil reutilizar o conteúdo, tornando a contribuição de outras comunidades menos provável. Outro problema com os cursos já presentes no GitHub é que o conteúdo é frequentemente armazenado no formato PDF. Embora amplamente utilizados para compartilhamento, os PDFs são tipicamente não editáveis, dificultando que os educadores modifiquem o conteúdo para suas necessidades específicas.

  

Nossa metodologia aborda esta limitação, criando uma estrutura de repositório genérica que é fácil de navegar, contribuir e reutilizar, mesmo por educadores não técnicos. Segundo nosso conhecimento, não existem outras metodologias propostas para organização e uso de recursos educacionais no ambiente de código aberto.

  

**4. METODOLOGIA** A metodologia que propomos oferece diretrizes para todos os níveis de interação com o repositório de um curso. Os sistemas de versionamento agrupam fundamentalmente as informações em repositórios. Como tal, consideramos que todos os recursos educativos relativos a um determinado curso ou área de estudo serão organizados num repositório.

  

**4.1 Tipos de Conteúdo** Os recursos educacionais vêm em vários formatos e tamanhos (como livros, wikis, vídeos, jogos de aprendizagem por computador e perguntas de múltipla escolha). Para poder navegar facilmente pelo conteúdo de um repositório, é imperativo que uma ampla gama de tipos seja suportada. Nós agrupamos os recursos nas seguintes 6 categorias amplas:

  

- **Reading (Leitura):** A forma mais comum de armazenar informações (livros, wikis, artigos). O conteúdo é desenvolvido para ser lido (texto) e é usado de forma autônoma ou em conjunto com outros tipos para explicar tópicos.
    
      
    
- **Media (Mídia):** Refere-se a materiais de áudio, visuais ou audiovisuais (imagens, gravações, vídeos, jogos). É um formato de fácil digestão, geralmente incorporado ao texto, slides ou projetos.
    
      
    
- **Slides:** Material de apoio principal para atividades ao vivo, como palestras, sessões práticas ou conferências, fornecendo suporte visual para apresentar informações e engajar os participantes (arquivos .pptx ou .ppt).
    
      
    
- **Guides (Guias):** Peças compostas por passos detalhados (tutoriais, demonstrações) para serem utilizados pelos alunos ou por educadores.
    
      
    
- **Drills (Exercícios Práticos):** Atividades destinadas a reforçar a aprendizagem através da prática repetitiva, como questionários, problemas e redações.
    
      
    
- **Projects (Projetos):** Itens práticos de maior escopo, que exigem mais tempo, esforço e recursos para serem concluídos (como tarefas de casa e trabalhos finais), divididos em etapas coerentes.
    
      
    

**4.2 Estrutura do Repositório** A estrutura do repositório deve ser fácil de navegar para que os educadores encontrem intuitivamente os recursos, facilitando também a seleção do conteúdo em qualquer nível de granularidade.

  

Nós criamos uma estrutura hierárquica rigorosa: os recursos de um curso são agrupados em "Capítulos" (_Chapters_). Cada capítulo é representado por uma série de "Tópicos" (_Topics_). Para cada tópico, existem os "Tipos de Conteúdo" (_Drills, Guides, Media, Projects, Reading, Slides_).

  

Ao usar esta forma de organização, os educadores podem navegar facilmente e selecionar os tópicos de interesse. Uma vez selecionado um tópico, todos os recursos pertencentes a ele serão incluídos no material de apresentação final com apenas um clique. Se algum conteúdo precisar ser excluído num nível mais granular (exercícios ou tarefas específicas), isso também é possível, mas de forma geral, os tópicos devem ser tratados como unidades indivisíveis.

  

Para os curadores e criadores, esta organização é vantajosa porque retira o fardo de ter de pensar sobre as dependências entre os tópicos. O tópico é criado e, se for necessário conhecimento prévio, pode ser inserido um simples link para outro tópico; é responsabilidade do educador estabelecer a ordem em que os conceitos são ensinados.

  

Por favor, responda com "next" para eu prosseguir com a etapa 3 da tradução.