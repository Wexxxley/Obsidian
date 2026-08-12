


---

- **Roadmap.sh:** Possui roadmaps para desenvolvedores. O conteúdo é EXCELENTE e possui praticamente tudo sobre TI. Porém, a plataforma em si é estática para o usuário final e só tem conteúdos de TI.
	- https://roadmap.sh/roadmaps
     ![500](../attachments/Pasted%20image%2020260812074955.png) ![](../attachments/Pasted%20image%2020260812075048.png)
- **Wikipedia (Curadoria Aberta):** A Wikipedia é o principal exemplo de curadoria de conteúdo descentralizada. O modelo de controle baseia-se na transparência absoluta: todas as edições são registradas em um histórico imutável. Para evitar inserções aleatórias ou vandalismo, a plataforma utiliza um sistema de moderação reativa. O conteúdo é publicado imediatamente, mas a comunidade possui ferramentas de reversão rápida.
	- https://www.wikipedia.org/
      
- **GitHub (Curadoria Fechada):** Diferente da Wikipedia, o GitHub adota um controle proativo. Através do conceito de Pull Request, as modificações propostas por terceiros ficam isoladas em um ambiente de aprovação. O código original permanece inalterado até que o mantenedor principal revise e autorize a mesclagem. Modelo mais seguro para roadmaps educacionais.
    - https://github.com/

- **Learn Anything:** O sistema estrutura tópicos educacionais em grafos, onde cada nó direciona o usuário para recursos didáticos específicos (artigos, cursos e documentações) curados pela própria comunidade. O Learn Anything centraliza o conteúdo em mapas globais (semelhante a uma estrutura unificada de wiki) e opera com a lógica de Teias de Conhecimento. No entanto, não há a imposição de uma ordem cronológica de consumo. A navegação é solta.
	- https://learn-anything.xyz/

- **Noção de Jardins digitais:** https://publish.obsidian.md/chicoary/2+-+%C3%81reas/Pessoal/Published/Tradu%C3%A7%C3%B5es/Uma+breve+hist%C3%B3ria+e+o+ethos+do+jardim+digital

Um **digital garden** (ou jardim digital) ==é um espaço online pessoal que mistura um caderno de notas com um blog, focado em cultivar ideias em público==. Ao contrário de um blog tradicional com posts fixos por ordem de data, ele é perene: as notas crescem, mudam e se conectam com links de forma livre ao longo do tempo. 

A noção de um digital garden está sendo usada há mais de duas décadas. No entanto, passou por algumas mudanças semânticas nesse período,

O ensaio de 1998 de Mark Bernstein parece ser a primeira menção registrada do termo. Mark fazia parte do grupo inicial de hipertexto, os desenvolvedores que estavam descobrindo como organizar e apresentar essa nova mídia. Embora o ensaio seja uma bela ode à exploração livre da Internet, ele não trata tanto da criação de espaços pessoais na Internet.

Os primeiros debates sobre isso na Web ficaram conhecidos como - a questão de como dar aos usuários da Web orientação suficiente para explorá-la livremente, sem forçá-los a experiências de navegação predefinidas. A eterna luta para encontrar o equilíbrio certo entre caos e estrutura. Após o ensaio de Mark, o termo **jardinagem digital** ficou em segundo plano por quase uma década.


Na Rede de Pesquisa em Aprendizagem Digital de 2015, Mike Caufield fez uma apresentação sobre . Posteriormente, ele estabeleceu as bases para nossa compreensão atual do termo. **Se alguém deve ser considerado a fonte original da _jardinagem digital_, é Caufield.** Ele foi o primeiro a expor toda essa ideia em palavras poéticas e coerentes.

Caufield deixa claro que a jardinagem digital não se trata de ferramentas específicas - não é um plug-in do Wordpress, um tema do Gastby ou um modelo do Jekyll. Trata-se de uma **maneira diferente de pensar sobre nosso comportamento on-line em relação às informações**, que acumula conhecimento pessoal ao longo do tempo em um espaço explorável.

O principal argumento de Caufield foi que nos deixamos levar pelos _streams_, o colapso das informações em linhas do tempo de eventos de trilha única. O design do feed de conversas das caixas de entrada de e-mail, dos bate-papos em grupo e do InstaTwitBook é efêmero - eles se preocupam apenas com pensamentos imediatos e autoafirmativos que passam por nós em poucos instantes.

Isso não é inerentemente ruim. As streams têm seu tempo e lugar. O Twitter é um multiplicador de força para pensamentos exploratórios e encontros agradáveis, uma vez que você se junta ao grupo certo e aprende a jogar o jogo.

No entanto, os fluxos de dados apenas trazem à tona as ideias do Zeitgeisty das últimas 24 horas. Eles não foram projetados para acumular conhecimento, conectar informações díspares ou amadurecer com o tempo.

O _jardim_ é o nosso contrapeso. **Os jardins apresentam informações em um cenário ricamente interligado que cresce lentamente com o tempo. Pense na maneira como a Wikipédia funciona quando você está pulando de um lugar para outro. É o melhor dos hiperlinks. Você pode escolher ativamente qual trilha de curiosidade seguir, em vez de seguir o fluxo efêmero filtrado por algoritmos.** O jardim nos ajuda a sair dos fluxos limitados pelo tempo e entrar em espaços de conhecimento contextual.



O que torna um site um jardin digital?


### 3. Papéis

- **Autor Oficial:** É o criador original do roadmap. Este personagem detém o poder de veto. A responsabilidade do mantenedor é definir a linha pedagógica da trilha, revisar as propostas enviadas e garantir que a estrutura permaneça coesa.
- **Colaborador:** Qualquer usuário autenticado no sistema. O colaborador consome o conteúdo, mas possui a permissão técnica para sugerir adições, correções de links quebrados ou remoção de tópicos obsoletos. A sua atuação é restrita à sugestão; nenhuma alteração proposta pelo colaborador afeta diretamente a versão oficial sem a aprovação do mantenedor.
- **Consumidor Final:** Usuário que utiliza a plataforma puramente para navegação e consumo do conteúdo, guiando-se pelas trilhas já consolidadas, sem envolvimento no processo de edição.

### **4. Fluxo Mínimo de Interação do Usuário**

1. **Descoberta e Consumo:** O estudante acessa a plataforma e busca um _roadmap_ público (por exemplo, "Matemática Discreta"). Ele visualiza a árvore de tópicos e inicia os estudos.
    
2. **Identificação de Lacuna:** Durante o estudo, o usuário percebe que um tópico específico está com um link desatualizado ou identifica um material mais didático na internet. O usuário decide atuar como Colaborador.
    
3. **Proposta de Alteração:** O colaborador aciona a interface de edição (isolada do original) e insere o novo link ou propõe um novo nó na árvore de dependências.
    - **Validação mínima Automatizada:** Antes mesmo do mantenedor revisar a sugestão, o sistema pode executar rotinas automatizadas básicas, como verificar se as URLs sugeridas pelo colaborador respondem com códigos de sucesso (HTTP 200), bloqueando a submissão de links quebrados ou endereços maliciosos.
    
4. **Validação e Aprovação:** O Mantenedor Oficial recebe uma notificação. A interface exibe a diferença visual exata. O mantenedor analisa, altera se quiser e clica em aprovar ou negar.
    
5. **Consolidação:** O sistema mescla as informações e o _roadmap_ oficial passa a exibir o novo material, registrando o crédito ao colaborador.
    