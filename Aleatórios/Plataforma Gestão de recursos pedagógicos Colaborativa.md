
**Ideia de nome: Acervo Mestre**

Repositório digital para que os professores de uma ou mais escolas/universidades possam cadastrar, organizar e compartilhar recursos pedagógicos (planos de aula, atividades, vídeos, slides, provas, etc). O Acervo Mestre centraliza, qualifica e facilita a evolução do material didático, transformando o esforço individual dos professores em um patrimônio intelectual duradouro para a escola.

### **1. MVP (Produto Mínimo Viável)**

1. **Cadastro de Recursos:**    
    - Upload de arquivos (PDF, DOCX, PPTX).
    - Permitir cadastro de links (vídeos do YouTube, artigos).
    - Permitir criação de "Recursos Simples" (apenas texto, como markdown).
        
2. **Sistema de Classificação (Taxonomia):**
    - **Tags:** `(ex: #prova, #exercicio-fixacao, #aula-invertida, #BNCC)`
    - **Categorias pré-definidas:** Disciplinas (Matemática, História), Ano/Série (6º Ano, 1ª Série EM), Tópicos (Geometria Espacial, Revolução Francesa).
        
3. **Busca e Filtros Avançados:**
    - O professor precisa encontrar o que procura.
    - Buscar por palavra-chave, filtrar por tags, categoria, disciplina, ano, formato do arquivo, etc.
        
4. **Curadoria e Organização (Playlists):**
    - Permitir a criação de coleções sequenciais de recursos (Playlists).
    - Permitir adicionar/remover recursos existentes do acervo a uma playlist.

---
### **2. Os Usuários**

##### **1. Professor:**
É o usuário principal.

- **Ações no MVP:**
    - **Pode fazer login** no sistema.
    - **Pode cadastrar** novos recursos de todos os tipos (arquivos, links, texto).
    - **Pode classificar** os recursos que ele mesmo criou (adicionar tags).
    - **Pode buscar e filtrar** por todos os recursos compartilhados na plataforma.
    - **Pode criar e gerenciar suas próprias playlists** (adicionar/remover recursos).
    - **Pode editar e excluir APENAS os seus próprios** recursos e playlists.

##### **2. Coordenador**
Responsável pela qualidade pedagógica de uma disciplina, série ou da escola como um todo. Ele garante que o conteúdo na plataforma seja relevante e de qualidade.

- **Ações no MVP:**
    - **Faz tudo que o Professor faz.**
    - **Moderação de Conteúdo:** Tem permissão para **editar ou excluir recursos de QUALQUER professor**.
        
##### **3. Gestor/ Diretor**:
É o cliente, quem "compra" a ideia do projeto.

---
### **3. Especificação de Requisitos**

#### **1. Requisitos Funcionais (RF)**
Os requisitos funcionais descrevem _o que_ o sistema deve fazer.

###### **RF-01: Gestão de Usuários e Autenticação**
- **RF-01.1:** O sistema deve permitir que usuários (Professores e Coordenadores) realizem login através de e-mail e senha.
- **RF-01.2:** O sistema deve diferenciar os níveis de permissão entre os papéis de "Professor" e "Coordenador".
- **RF-01.3:** O sistema deve manter a sessão do usuário ativa após o login.

###### **RF-02: Gestão de Recursos Pedagógicos (CRUD)**
- **RF-02.1:** O sistema deve permitir o cadastro de novos recursos pedagógicos de três tipos:
    - a) Upload de arquivo (formatos permitidos: PDF, DOCX, PPTX).
    - b) Link externo (URL, ex: vídeos do YouTube, artigos).
    - c) Recurso de texto simples (criado em um editor de texto no próprio sistema, com suporte a Markdown).
- **RF-02.2:** Ao cadastrar um recurso, o usuário deve ser obrigado a preencher campos de classificação (Categorias pré-definidas).
- **RF-02.3:** O sistema deve permitir que o autor de um recurso o edite a qualquer momento.
- **RF-02.4:** O sistema deve permitir que o autor de um recurso o exclua a qualquer momento.

###### **RF-03: Sistema de Classificação (Taxonomia)**
- **RF-03.1:** O sistema deve permitir que, durante o cadastro ou edição de um recurso, o usuário associe uma ou mais **tags** de forma livre (ex: `#prova`, `#BNCC`).
- **RF-03.2:** O sistema deve prover **categorias pré-definidas e obrigatórias** para a classificação dos recursos, incluindo:
    - a) Disciplina (ex: Matemática, História).
    - b) Série (ex: 6º Ano, 1ª Série EM).
    - c) Tópico (ex: Geometria Espacial, Revolução Francesa).

###### **RF-04: Busca e Filtragem**
- **RF-04.1:** O sistema deve possuir um campo de busca por palavra-chave que pesquise nos títulos e descrições dos recursos.
- **RF-04.2:** O sistema deve permitir a aplicação de múltiplos filtros para refinar os resultados da busca, incluindo:
    - a) Filtrar por Tags.
    - b) Filtrar por Disciplina.
    - c) Filtrar por Série.
    - d) Filtrar por Formato do Recurso (Arquivo, Link, Texto).

###### **RF-05: Moderação de Conteúdo (Privilégios do Coordenador)**
- **RF-05.1:** Um usuário com o papel de "Coordenador" deve ter a permissão para editar as informações e o conteúdo de qualquer recurso cadastrado por qualquer professor.
- **RF-05.2:** Um usuário com o papel de "Coordenador" deve ter a permissão para excluir qualquer recurso cadastrado por qualquer professor

###### **RF-06: Gestão de Playlists**
- **RF-06.1:** O sistema deve permitir que um Professor crie uma nova playlist, definindo um título e uma descrição.
- **RF-06.2:** O sistema deve permitir que um Professor adicione recursos existentes no acervo a uma de suas playlists.
- **RF-06.3:** O sistema deve permitir que o proprietário de uma playlist remova recursos dela e edite suas informações (título e descrição).
- **RF-06.4:** O sistema deve permitir que o proprietário de uma playlist a exclua.

#### **2. Requisitos Não-Funcionais (RNF)**
Os requisitos não-funcionais descrevem _como_ o sistema deve operar, definindo seus atributos de qualidade.

- **RNF-01 (Usabilidade):** A interface do sistema deve ser intuitiva e clara, exigindo o mínimo de treinamento para que um professor consiga cadastrar e buscar recursos.
- **RNF-02 (Desempenho):** As buscas e filtragens de recursos devem retornar resultados em menos de 3 segundos.
- **RNF-03 (Segurança):** O acesso ao acervo deve ser restrito a usuários autenticados da escola ou rede de escolas. Os dados dos usuários (senhas) devem ser armazenados de forma criptografada.
- **RNF-04 (Compatibilidade):** A plataforma deve ser totalmente funcional nas versões mais recentes dos principais navegadores web (Google Chrome, Mozilla Firefox, Microsoft Edge).

---
### **4. Especificação de Histórias de Usuário**
Histórias de usuário focam na perspectiva do usuário final, descrevendo uma funcionalidade, seu motivo e o valor gerado.

#### **1. Gerenciamento de Recursos Pedagógicos**

- **HU-01:** Como um **Professor**, eu quero **fazer o upload de um plano de aula em PDF** para que **outros colegas da mesma disciplina possam aproveitá-lo e eu não precise enviá-lo por e-mail**.
    
- **HU-02:** Como um **Professor**, eu quero **cadastrar o link de um vídeo educativo do YouTube** para que **possa centralizar as referências da minha aula em um único lugar**.
    
- **HU-03:** Como um **Professor**, eu quero **escrever uma pequena anotação diretamente na plataforma** para que **eu possa compartilhar uma ideia rapidamente, sem precisar criar um arquivo formal**.
    
- **HU-04:** Como um **Professor**, eu quero **adicionar as tags e a um recurso que cadastrei** para que **seja mais fácil para mim e para outros encontrá-lo no futuro**.
    
- **HU-05:** Como um **Professor**, eu quero **excluir um recurso que se tornou obsoleto** para que **o acervo se mantenha atualizado e relevante**.
    
- **HU-06:** Como um **Coordenador**, eu quero **gerenciar(CRUD) um conteúdo de um professor** para que **eu possa garantir que ele está alinhado com o projeto pedagógico da escola**.
    
- **HU-07:** Como um **Professor**, eu quero **poder editar o conteúdo de um recurso do tipo "anotação" que eu criei** para que **eu possa refinar minhas ideias ou corrigir informações diretamente na plataforma**.
    
- **HU-08:** Como um **Professor**, eu quero **criar uma nova playlist com um título e uma descrição** para que **eu possa ter um espaço definido para agrupar os recursos de uma aula específica, como "Ecossistemas Brasileiros"**.
    
- **HU-09:** Como um **Professor**, eu quero **ter um botão "Adicionar à Playlist" em cada recurso do acervo** para que **eu possa facilmente adicionar materiais que encontro a uma ou mais das minhas playlists existentes**.

#### **2. Descoberta e Uso de Recursos**

- **HU-10:** Como um **Professor**, eu quero **buscar por "Revolução Francesa"** para que **eu possa encontrar rapidamente todos os materiais disponíveis sobre esse tema para minha aula**.
    
- **HU-11:** Como um **Professor**, eu quero **filtrar os recursos por Matéria, Série e formato** para que **eu possa encontrar apenas o necessário para minha aula**.
    
- **HU-12:** Como um **Professor ou Coordenador**, eu quero **visualizar e baixar um recurso que encontrei na busca** para que **eu possa usá-lo**.
    
- **HU-13:** Como um **Professor**, eu quero **ver os recursos mais recentes adicionados na página inicial ao fazer login** para que **eu possa me manter atualizado com as novidades sem precisar fazer uma busca**.
    
- **HU-14:** Como um **Coordenador**, eu quero **poder "destacar" um recurso para que ele apareça em evidência na página inicial** para que **todos os professores vejam um material de alta qualidade ou relevância para o período letivo**.

#### **3. Interação e Melhoria Contínua**

- **HU-15:** Como um **Professor**, eu quero **ver o nome do autor de cada recurso listado** para que **eu saiba a quem procurar para tirar dúvidas ou dar feedback pessoalmente**.
    
- **HU-16:** Como um **Professor**, eu quero **ver um contador de visualizações e downloads em cada recurso** para que **eu tenha uma noção da popularidade e utilidade dos materiais**.
    
#### **4. Acesso e Gestão de Usuários**

- **HU-17:** Como um **Professor ou Coordenador**, eu quero **fazer login no sistema de forma segura e rápida** para que **eu possa acessar o acervo de materiais exclusivos da minha escola**.
    
- **HU-18:** Como um **Gestor ou Coordenador**, eu quero **cadastrar um novo professor na plataforma, associando-o à nossa escola** para que **ele tenha acesso imediato ao acervo e possa começar a colaborar**.
    
- **HU-19:** Como um **Gestor ou Coordenador**, eu quero **desativar o acesso de um professor que não faz mais parte da equipe** para que **a segurança e a privacidade dos nossos materiais sejam mantidas**.
    

#### **5. Visão de Gestão (Cliente)**

- **HU-20:** Como um **Gestor de Escola**, eu quero **ter uma plataforma onde o conhecimento pedagógico dos meus professores é centralizado e compartilhado** para que **a qualidade do ensino seja padronizada e o esforço individual se torne um patrimônio duradouro da instituição**.