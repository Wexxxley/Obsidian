*Especificação de Requisitos – Plataforma Acervo Mestre*

 *1. Perfis de Usuário*

* *Professor:* Usuário principal do sistema. Responsável por criar, organizar, buscar e utilizar os recursos pedagógicos.
* *Coordenador:* Responsável pela curadoria e qualidade pedagógica do acervo. Possui todas as permissões de um Professor, com poderes adicionais de moderação sobre o conteúdo de outros usuários.
* *Gestor:* Administrador do sistema. Responsável pela gestão de usuários e pela padronização dos metadados da plataforma.

*2. Requisitos Funcionais (RF)*

Os requisitos funcionais descrevem as funcionalidades e comportamentos que o sistema deve executar.

 *RF-01: Gestão de Usuários e Autenticação*
* *RF-01.1:* O sistema deve permitir que usuários (Professor, Coordenador) se autentiquem através de e-mail institucional e senha. *[US-17]*
* *RF-01.2:* O sistema deve possuir uma área restrita, acessível apenas após a autenticação bem-sucedida. *[US-17]*
* *RF-01.3:* O Gestor deve ser capaz de cadastrar novos usuários (Professores, Coordenadores), associando-os a uma escola e/ou disciplinas. *[US-18]*
* *RF-01.4:* O Gestor deve ser capaz de desativar o acesso de um usuário ao sistema, garantindo a segurança da informação. *[US-19]*
* *RF-01.5:* O sistema deve diferenciar as permissões de acesso e ações com base no perfil do usuário (Professor, Coordenador, Gestor).

 *RF-02: Gestão de Recursos Pedagógicos (CRUD)*
* *RF-02.1 (Criar):* O Professor deve poder cadastrar novos recursos de três formas distintas:
    a. *Upload de Arquivo:* Enviando arquivos nos formatos PDF, DOCX, PPTX e MP4, com um título e uma descrição associados. *[US-1]*
    b. *URL Externa:* Cadastrando um link (ex: YouTube, Vimeo, artigo online) com título e descrição. *[US-2]*
    c. *Nota Simples:* Criando um recurso de texto puro utilizando a sintaxe Markdown, com título. *[US-3]*
* *RF-02.2 (Visualizar/Ler):* Usuários autenticados devem poder visualizar e baixar os recursos para os quais têm permissão. *[US-12]*
* *RF-02.3 (Editar):*
    a. O Professor deve poder editar os metadados (título, descrição, tags) e o conteúdo dos recursos que ele mesmo criou. *[US-7]*
    b. O Coordenador deve poder editar os metadados e o conteúdo de qualquer recurso na plataforma. *[US-6]*
* *RF-02.4 (Excluir):*
    a. O Professor (autor) deve poder excluir permanentemente os recursos que ele mesmo criou. *[US-5]*
    b. O Coordenador deve poder excluir ou despublicar qualquer recurso da plataforma. *[US-6]*

 *RF-03: Busca e Descoberta de Recursos*
* *RF-03.1:* O sistema deve permitir a busca de recursos por palavras-chave presentes no título ou descrição. *[US-10]*
* *RF-03.2:* O sistema deve fornecer filtros para refinar os resultados da busca por Matéria, Série/Ano e Formato do recurso. *[US-11]*
* *RF-03.3:* A plataforma deve exibir uma seção com os recursos publicados mais recentemente, permitindo que os professores se mantenham atualizados. *[US-13]*

 *RF-04: Organização e Curadoria (Taxonomia e Playlists)*
* *RF-04.1:* O Professor deve poder atribuir uma ou mais tags a um recurso no momento do cadastro ou edição. *[US-4]*
* *RF-04.2:* O Professor deve poder criar "Playlists", que são coleções ordenadas de recursos, contendo um título e uma descrição. *[US-8]*
* *RF-04.3:* O Professor deve poder adicionar e remover recursos de suas próprias playlists. **[US-9]**
* *RF-04.4:* O Coordenador deve poder marcar um recurso como "Destaque" para que ele ganhe visibilidade na plataforma. *[US-14]*

 *RF-05: Informações de Recurso e Métricas*
* *RF-05.1:* Ao visualizar um recurso, o sistema deve exibir o nome do autor e seu contato institucional. *[US-15]*
* *RF-05.2:* O sistema deve registrar e exibir contadores de visualizações e downloads para cada recurso. *[US-16]*

*RF-06: Administração da Plataforma*
* *RF-06.1:* O Gestor deve ter uma interface para gerenciar (criar, editar, remover) os valores padrão para os metadados de Matéria, Série/Ano e Formato, garantindo a consistência do acervo. *[US-20]*

*3. Requisitos Não-Funcionais (RNF)*

Os requisitos não-funcionais descrevem os critérios de qualidade e operação do sistema.

* *RNF-01 (Usabilidade):* A interface deve ser intuitiva e de fácil utilização para professores e coordenadores, que podem ter diferentes níveis de familiaridade com tecnologia.
* *RNF-02 (Desempenho):*
    O tempo de resposta para buscas e filtros deve ser inferior a 3 segundos.
    O upload e download de arquivos deve ser eficiente, com feedback visual claro para o usuário durante o processo.
* *RNF-03 (Segurança):*
    O acesso aos recursos e funcionalidades deve ser estritamente controlado pelos perfis de usuário definidos.
    O sistema deve proteger os dados dos usuários e os arquivos armazenados contra acesso não autorizado.
* *RNF-04 (Compatibilidade):* A plataforma deve ser compatível com os principais navegadores de mercado em suas versões mais recentes (Google Chrome, Mozilla Firefox, Microsoft Edge).
* *RNF-05 (Disponibilidade):* O sistema deve estar disponível para acesso 99% do tempo, excluindo janelas de manutenção planejadas.

opiniões sobre esses requisitos