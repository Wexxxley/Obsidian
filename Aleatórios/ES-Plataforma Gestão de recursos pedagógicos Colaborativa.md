
**Ideia de nome: Acervo Mestre**

Repositório digital para que os professores de uma ou mais escolas/universidades possam cadastrar, organizar e compartilhar recursos pedagógicos (planos de aula, atividades, vídeos, slides, provas, etc). O Acervo Mestre centraliza, qualifica e facilita a evolução do material didático, transformando o esforço individual dos professores em um patrimônio intelectual duradouro para a escola.

---
### **1. Os Usuários**

- **Professor**: Usuário principal do sistema. Responsável por criar, organizar, buscar e utilizar os recursos pedagógicos.
* **Coordenador**: Responsável pela curadoria e qualidade pedagógica do acervo. Possui todas as permissões de um Professor, com poderes adicionais de moderação sobre o conteúdo de outros usuários.
* **Gestor**: Administrador do sistema. Responsável pela gestão de usuários e pela padronização dos metadados da plataforma.

---
### 2. Requisitos Funcionais (RF)

 **RF-01: Gestão de Usuários e Autenticação**
* RF-01.1: O sistema deve permitir que usuários (Professor, Coordenador) se autentiquem através de e-mail institucional e senha. 
* RF-01.2: O sistema deve possuir uma área restrita, acessível apenas após a autenticação bem-sucedida. 
* RF-01.3: O Gestor deve ser capaz de cadastrar novos usuários (Professores, Coordenadores).
* RF-01.4: O Gestor deve ser capaz de desativar o acesso de um usuário ao sistema, garantindo a segurança da informação.
* RF-01.5: O sistema deve diferenciar as permissões de acesso e ações com base no perfil do usuário (Professor, Coordenador, Gestor).

 **RF-02: Gestão de Recursos Pedagógicos (CRUD)**
* RF-02.1 (Criar): O Professor deve poder cadastrar novos recursos de três formas distintas:
    a. Upload de Arquivo: Enviando arquivos nos formatos PDF, DOCX, PPTX e MP4, com um título e uma descrição associados. 
    b. URL Externa: Cadastrando um link (ex: YouTube, Vimeo, artigo online) com título e descrição. 
    c. Nota Simples: Criando um recurso de texto puro utilizando a sintaxe Markdown, com título. 
* RF-02.2 (Visualizar/Ler): Usuários autenticados devem poder visualizar e baixar os recursos para os quais têm permissão. 
* RF-02.3 (Editar):
    a. O Professor deve poder editar os metadados (título, descrição, tags) e o conteúdo dos recursos que ele mesmo criou. 
    b. O Coordenador deve poder editar os metadados e o conteúdo de qualquer recurso na plataforma. 
* RF-02.4 (Excluir):
    a. O Professor (autor) deve poder excluir permanentemente os recursos que ele mesmo criou. 
    b. O Coordenador deve poder excluir ou despublicar qualquer recurso da plataforma. [US-6]

 **RF-03: Busca e Descoberta de Recursos**
* RF-03.1: O sistema deve permitir a busca de recursos por palavras-chave presentes no título ou descrição. 
* RF-03.2: O sistema deve fornecer filtros para refinar os resultados da busca por Matéria e Formato do recurso. 
* RF-03.3: A plataforma deve exibir uma seção com os recursos publicados mais recentemente, permitindo que os professores se mantenham atualizados. 

 **RF-04: Organização e Curadoria (Taxonomia e Playlists)**
* RF-04.1: O Professor deve poder atribuir uma ou mais tags a um recurso no momento do cadastro ou edição. 
* RF-04.2: O Professor deve poder criar "Playlists", que são coleções ordenadas de recursos, contendo um título e uma descrição.
* RF-04.3: O Professor deve poder adicionar e remover recursos de suas próprias playlists. 
* RF-04.4: O Coordenador/gestor deve poder marcar um recurso como "Destaque" para que ele ganhe visibilidade na plataforma. 

 **RF-05: Informações de Recurso e Métricas**
* RF-05.1: Ao visualizar um recurso, o sistema deve exibir o nome do autor e seu contato institucional. 
* RF-05.2: O sistema deve registrar e exibir contadores de visualizações e downloads para cada recurso.

**RF-06: Administração da Plataforma**
* RF-06.1: O Gestor deve ter uma interface para gerenciar (criar, editar, remover) os valores padrão para os metadados de Matéria e  Formato, garantindo a consistência do acervo. 

--- 
### 3. Requisitos Não-Funcionais (RNF)

Os requisitos não-funcionais descrevem os critérios de qualidade e operação do sistema.

* RNF-01 (Usabilidade): A interface deve ser intuitiva e de fácil utilização para professores e coordenadores, que podem ter diferentes níveis de familiaridade com tecnologia.
* RNF-02 (Desempenho):
    O tempo de resposta para buscas e filtros deve ser inferior a 3 segundos.
    O upload e download de arquivos deve ser eficiente, com feedback visual claro para o usuário durante o processo.
* RNF-03 (Segurança):
    O acesso aos recursos e funcionalidades deve ser estritamente controlado pelos perfis de usuário definidos.
    O sistema deve proteger os dados dos usuários e os arquivos armazenados contra acesso não autorizado.
* RNF-04 (Compatibilidade): A plataforma deve ser compatível com os principais navegadores de mercado em suas versões mais recentes (Google Chrome, Mozilla Firefox, Microsoft Edge).
* RNF-05 (Disponibilidade): O sistema deve estar disponível para acesso 99% do tempo, excluindo janelas de manutenção planejadas.
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


---
### **1. Perfis de Usuário**

- **Professor:** Usuário principal do sistema. Responsável por criar (públicos ou privados), organizar, buscar e utilizar os recursos pedagógicos. Pode visualizar todos os recursos.
- **Coordenador:** Responsável pela curadoria e qualidade pedagógica. Possui todas as permissões de um Professor, com poderes adicionais de moderação (editar/excluir) sobre o conteúdo de outros usuários. Pode visualizar todos os recursos.
- **Gestor:** Administrador do sistema. Responsável pela gestão de todos os usuários (incluindo Alunos) e pela padronização dos metadados. Pode visualizar todos os recursos.
- **Aluno:** Usuário com o menor nível de acesso. Responsável por consumir conteúdo. Pode autenticar-se, buscar, visualizar e baixar **apenas** os recursos marcados como `Públicos`.

---

### **2. Requisitos Funcionais (RF)**

Os requisitos funcionais descrevem as funcionalidades e comportamentos que o sistema deve executar.

#### **RF-01: Gestão de Usuários e Autenticação**

- RF-01.1: O sistema deve permitir que usuários se autentiquem através de e-mail e senha.
- RF-01.2: O sistema deve possuir uma área restrita, acessível apenas após a autenticação bem-sucedida. 
- RF-01.3: O Gestor deve ser capaz de cadastrar novos usuários (Professores, Coordenadores, Alunos).
- RF-01.4: O Gestor deve ser capaz de desativar o acesso de um usuário (de qualquer perfil) ao sistema, garantindo a segurança da informação.  
- RF-01.5: O sistema deve diferenciar as permissões de acesso e ações com base no perfil do usuário (Professor, Coordenador, Gestor, Aluno*).

#### **RF-02: Gestão de Recursos Pedagógicos (CRUD) (Atualizado)**

- **RF-02.0 (Novo): Controle de Visibilidade**
    
    - **RF-02.0.1:** Todo recurso pedagógico no sistema deve possuir um estado de visibilidade: `Público` ou `Privado`.
        
    - **RF-02.0.2:** O estado padrão de um novo recurso ao ser criado deve ser `Privado`, para garantir a segurança e curadoria antes da exposição.
        
    - **RF-02.0.3:** Usuários com perfil `Aluno` podem apenas visualizar e baixar recursos marcados como `Público`.
        
    - **RF-02.0.4:** Usuários com perfil `Professor`, `Coordenador` e `Gestor` podem visualizar, baixar e gerenciar todos os recursos, independentemente da visibilidade.
        
- RF-02.1 (Criar): O Professor deve poder cadastrar novos recursos...
    
    - a. Upload de Arquivo...
        
    - b. URL Externa...
        
    - c. Nota Simples...
        
    - **RF-02.1.1 (Novo):** Ao criar ou editar um recurso (conforme RF-02.1 e RF-02.3), o Professor deve poder definir sua visibilidade (`Público` ou `Privado`).
        
- RF-02.2 (Visualizar/Ler): O acesso para visualização e download de recursos **é regido pelas regras de visibilidade (RF-02.0)** e pelo perfil do usuário. [US-12]
    
- RF-02.3 (Editar):
    
    - a. O Professor deve poder editar os metadados (título, descrição, tags), **a visibilidade (Público/Privado)** e o conteúdo dos recursos que ele mesmo criou. [US-7]
        
    - b. O Coordenador deve poder editar os metadados, **a visibilidade** e o conteúdo de qualquer recurso na plataforma. [US-6]
        
- RF-02.4 (Excluir):
    
    - a. O Professor (autor) deve poder excluir...
        
    - b. O Coordenador deve poder excluir...
        
    - _(Nota: Alunos não podem criar, editar ou excluir recursos.)_
        

#### **RF-03: Busca e Descoberta de Recursos (Atualizado)**

- RF-03.1: O sistema deve permitir a busca de recursos... **Os resultados da busca para um `Aluno` devem conter apenas recursos `Públicos`.** [US-10]
    
- RF-03.2: O sistema deve fornecer filtros para refinar os resultados... A lógica de filtragem deve respeitar as regras de visibilidade do perfil (ex: um `Aluno` filtrando por "Matemática" só verá recursos `Públicos` de Matemática). [US-11]
    
- RF-03.3: A plataforma deve exibir uma seção com os recursos publicados mais recentemente... **Para o perfil `Aluno`, esta seção deve exibir apenas recursos `Públicos`.** [US-13]
    

#### **RF-04: Organização e Curadoria (Taxonomia e Playlists) (Atualizado)**

- RF-04.1: O Professor deve poder atribuir... [US-4]
    
- RF-04.2: O Professor deve poder criar "Playlists"... [US-8]
    
- RF-04.3: O Professor deve poder adicionar e remover recursos... [US-9]
    
- RF-04.4: O Coordenador deve poder marcar um recurso como "Destaque"... **A exibição de "Destaques" para um `Aluno` deve ser restrita a recursos `Públicos`.** [US-14]
    
- **RF-04.5 (Novo):** O perfil `Aluno` não pode criar, editar ou gerenciar tags ou playlists.
    

#### **RF-05: Informações de Recurso e Métricas**

- RF-05.1: Ao visualizar um recurso (ao qual tem permissão), o sistema deve exibir o nome do autor e seu contato institucional. [US-15]
    
- RF-05.2: O sistema deve registrar e exibir contadores de visualizações e downloads para cada recurso. [US-16]
    

#### **RF-06: Administração da Plataforma**

- RF-06.1: O Gestor deve ter uma interface para gerenciar... [US-20] _(Nota: Esta área é inacessível para Alunos.)_
    

---

### **3. Requisitos Não-Funcionais (RNF) (Atualizado)**

- RNF-01 (Usabilidade): A interface deve ser intuitiva...
    
- RNF-02 (Desempenho): O tempo de resposta para buscas e filtros...
    
- RNF-03 (Segurança):
    
    - O acesso aos recursos e funcionalidades deve ser estritamente controlado pelos perfis de usuário definidos.
        
    - O sistema deve proteger os dados dos usuários e os arquivos...
        
    - **RNF-03.1 (Novo):** O sistema deve garantir rigorosamente que usuários com perfil `Aluno` não possam, sob nenhuma circunstância (ex: manipulação de ID na URL ou API), aceder, visualizar ou baixar recursos marcados como `Privados`.
        
- RNF-04 (Compatibilidade): A plataforma deve ser compatível...
    
- RNF-05 (Disponibilidade): O sistema deve estar disponível...



---


User(id, nome, email, senha_hash, perfil)