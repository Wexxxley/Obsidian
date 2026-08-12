


---

- **Roadmap.sh:** Possui roadmaps para desenvolvedores. O conteúdo é EXCELENTE e possui praticamente tudo sobre TI. Porém, a plataforma em si é estática para o usuário final e só tem conteúdos de TI.
	- https://roadmap.sh/roadmaps
     ![500](../attachments/Pasted%20image%2020260812074955.png) ![](../attachments/Pasted%20image%2020260812075048.png)
- **Wikipedia (Curadoria Aberta):** A Wikipedia é o principal exemplo de curadoria de conteúdo descentralizada. O modelo de controle baseia-se na transparência absoluta: todas as edições são registradas em um histórico imutável. Para evitar inserções aleatórias ou vandalismo, a plataforma utiliza um sistema de moderação reativa. O conteúdo é publicado imediatamente, mas a comunidade possui ferramentas de reversão rápida. 
	- https://www.wikipedia.org/
      
- **GitHub (Curadoria Fechada):** Diferente da Wikipedia, o GitHub adota um controle proativo. Através do conceito de Pull Request, as modificações propostas por terceiros ficam isoladas em um ambiente de aprovação. O código original permanece inalterado até que o mantenedor principal revise e autorize a mesclagem. Modelo mais seguro para roadmaps educacionais.
    - https://github.com/ossu/computer-science-br **OSSU (Open Source Society University):** É um dos repositórios mais famosos do GitHub. Eles construíram um roadmap completo de graduação em Ciência da Computação utilizando apenas cursos gratuitos (tem a versão BR). A estrutura é um documento linear de texto, mas a governança é altamente colaborativa.

- **Learn Anything:** O sistema estrutura tópicos educacionais em grafos, onde cada nó direciona o usuário para recursos didáticos específicos (artigos, cursos e documentações) curados pela própria comunidade. O Learn Anything centraliza o conteúdo em mapas globais (semelhante a uma estrutura unificada de wiki) e opera com a lógica de Teias de Conhecimento. No entanto, não há a imposição de uma ordem cronológica de consumo. A navegação é solta.
	- https://learn-anything.xyz/

- **Noção de Jardins digitais:** https://publish.obsidian.md/chicoary/2+-+%C3%81reas/Pessoal/Published/Tradu%C3%A7%C3%B5es/Uma+breve+hist%C3%B3ria+e+o+ethos+do+jardim+digital
	Um roadmap criado por um autor X na plataforma não seria considerado um jardin digital pois um jardin digital deve ter: "Muitos pontos de entrada, mas **nenhum caminho prescrito**." Embora compartilhe alguns conceitos como:
	- Ambos tratam o conhecimento como um espaço a ser mapeado.
    - Crescimento Contínuo
    - Fuga do Formato Padrão em favor de uma rede de recursos interligados.

	O conceito de Digital Garden serve para compor a seção de "Trabalhos Relacionados". É possivel   citar o movimento de Digital Gardening (e autores como Mike Caulfield) para demonstrar que a internet já percebeu a necessidade de organizar o conhecimento em redes em vez de feeds. Embora os Jardins Digitais resolvam o problema do armazenamento relacional, eles falham em guiar o estudante iniciante devido à ausência de caminhos prescritos.

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
    