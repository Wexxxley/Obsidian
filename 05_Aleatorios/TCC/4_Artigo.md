
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