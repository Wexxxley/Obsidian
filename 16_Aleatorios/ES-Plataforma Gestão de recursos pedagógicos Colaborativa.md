
**Ideia de nome: Acervo Mestre**

Repositório digital para que os professores de uma ou mais escolas/universidades possam cadastrar, organizar e compartilhar recursos pedagógicos (planos de aula, atividades, vídeos, slides, provas, etc). O Acervo Mestre centraliza, qualifica e facilita a evolução do material didático, transformando o esforço individual dos professores em um patrimônio intelectual duradouro para a escola.

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
    
