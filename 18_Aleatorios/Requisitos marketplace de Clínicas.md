
---

- **Escopo**: Consulta e exames. A plataforma atua como intermediário entre o paciente e a clínica e a cobrança é individual para cada clínica.
- Não vamos considerar convênio.
- O cadastro de clinicas é feito pelos admins do sistema.
- O processamento do pagamento da consulta/exame fica pela clínica.
### **1. Módulo do Paciente**

**[RF01] Cadastro e Login** **Descrição:** Como Paciente, quero criar uma conta e acessar o sistema para gerenciar meus agendamentos. 

**Fluxo Principal:**
1. Usuário acessa a opção "Cadastrar".
2. Insere: Nome Completo, CPF, E-mail, Telefone e Endereço.
3. Define uma senha de acesso.
4. Sistema valida a unicidade do CPF e E-mail.
5. Usuário realiza o login com CPF/E-mail e Senha. 

**Fluxos Alternativos:**    
- **FA01:** CPF inválido ou já cadastrado (O sistema impede o registro e sinaliza o erro).
- **FA02:** Senha incorreta (O sistema bloqueia o acesso e sugere recuperação).
 
**Mensagens do Sistema:**    
- **MSG01:** "Cadastro realizado com sucesso!" 

---

**[RF02] Buscar Consultas e Exames**: Como Paciente, quero pesquisar por especialidades, procedimentos ou nomes de clínicas para encontrar o atendimento necessário. 

**Fluxo Principal:**
1. Usuário acessa a barra de busca na tela inicial.
2. Digita o termo de busca (ex: "Cardiologia" ou "Exame de Sangue").
3. O sistema utiliza a geolocalização para filtrar resultados próximos.
4. O sistema exibe uma lista de clínicas com distância, serviços e nota. 

**Fluxos Alternativos:**
- **FA01:** Geolocalização desativada (O sistema solicita a inserção do CEP ou cidade manualmente). **Mensagens do Sistema:**
    
- **MSG01:** "Nenhum prestador encontrado nesta região." 

**Critérios de Aceitação:** A busca deve permitir filtros por "Tipo" e "Preço".

---

**[RF03] Agendar Consulta/Exame** **Descrição:** Como Paciente, quero selecionar um serviço para ser direcionado ao canal de atendimento da clínica.

**Fluxo Principal:**
1. Usuário visualiza a lista de serviços de uma clínica específica.
2. Seleciona o serviço desejado (Ex: Hemograma).
3. O sistema apresenta um formulário com mensagem pré-definida contendo os dados do paciente.
4. Usuário clica em "Confirmar".
5. O sistema redireciona o usuário para o WhatsApp ou Site externo da clínica. 

**Fluxos Alternativos:**
- **FA01:** Clínica sem link de redirecionamento configurado (O sistema exibe o telefone de contato direto). 

**Critérios de Aceitação:** O redirecionamento deve carregar a mensagem formatada para agilizar o atendimento externo.

---

**[RF04] Acessar Perfil da Clínica**: Como Paciente, quero visualizar informações detalhadas da clínica e seus profissionais antes de decidir pelo agendamento. 

**Fluxo Principal:**
1. Usuário clica em uma clínica no resultado da busca.
2. Sistema exibe: Fotos, Descrição, Localização, Corpo Clínico (profissionais) e Catálogo de Serviços.
3. Usuário navega entre as abas de "Informações" e "Avaliações". 

---

**[RF05] Feedback para a Clínica**: Como Paciente, quero avaliar o atendimento e a infraestrutura da clínica visitada. 

**Fluxo Principal:**
1. Usuário acessa o perfil da clínica.
2. Seleciona a opção "Avaliar/Feedback".
3. Escolhe uma nota (1 a 5 estrelas) e escreve um comentário.
4. Salva a avaliação.

**Critérios de Aceitação:** O comentário deve passar por um filtro de palavras ofensivas.

---
### **2. Módulo da Clínica**

**[RF06] Edição de Informações do Perfil**: Como Profissional/Gestor, quero manter os dados da clínica atualizados para atrair pacientes. 

**Fluxo Principal:**
1. Usuário (Clínica) acessa "Meu Perfil".    
2. Edita campos como: Horário de Funcionamento, Localização, Descrição e Fotos.
3. Gerencia "Profissionais": Adiciona ou remove nomes e especialidades.
4. Gerencia "Serviços": Adiciona consultas e exames oferecidos.

**Mensagens do Sistema:**
- **MSG01:** "Perfil atualizado com sucesso." 

**Critérios de Aceitação:** Alterações de localização devem atualizar automaticamente as coordenadas de geolocalização para busca.

---

**[RF07] Upload de Resultados/Documentos** **Descrição:** Como Profissional, quero disponibilizar resultados de exames digitalizados diretamente para o paciente. 

**Fluxo Principal:**
1. Usuário (Clínica) acessa a área de "Documentos/Laudos".
2. Seleciona a opção "Fazer Upload".
3. Insere o CPF do paciente destinatário.
4. Seleciona o arquivo (PDF ou Imagem) do dispositivo.
5. Confirma o envio. 

**Fluxos Alternativos:**
- **FA01:** CPF não encontrado na base de dados (O sistema alerta que o paciente não possui cadastro)

**Mensagens do Sistema:**    
- **MSG01:** "Arquivo enviado com sucesso para o paciente." **

**Critérios de Aceitação:**** O arquivo deve ser armazenado em ambiente criptografado e ficar disponível apenas para o CPF informado através de login seguro.

No Brasil, o tratamento de dados de saúde exige consentimento explícito. Recomendo adicionar um termo de aceite no **RF01** para o paciente autorizar o recebimento de laudos via plataforma.

---
### **3. Módulo Administrativo (Gestor Único)**

**[RF08] Painel de Controle de Clínicas**: Como Administrador, quero cadastrar, ativar ou suspender clínicas para controlar quem aparece na plataforma para os pacientes. 

**Fluxo Principal:**
1. Administrador acessa "Lista de Clínicas".
2. Seleciona "Adicionar Clínica".
3. Insere: CNPJ, Razão Social, E-mail do responsável e Endereço.
4. O sistema gera as credenciais de acesso e envia ao e-mail da clínica.
5. Administrador altera o status para "Ativo". 

**Fluxos Alternativos:**
- **FA01:** Suspensão de Clínica (O Administrador altera o status para "Suspenso", removendo a clínica das buscas dos pacientes e bloqueando o painel da clínica).

**Mensagens do Sistema:**    
- **MSG01:** "Clínica cadastrada e credenciais enviadas." 

**Critérios de Aceitação:** O sistema deve validar o formato do CNPJ e garantir que o e-mail seja único.

---

**[RF09] Configuração Financeira Individual**: Como Administrador, quero definir o valor da cobrança para cada clínica e monitorar o status de pagamento. 

**Fluxo Principal:**
1. Administrador acessa o perfil de uma clínica cadastrada.    
2. Define o valor da mensalidade acordada.
3. Insere a data de vencimento.
4. O sistema exibe o status financeiro (Em dia / Pendente). 

**Critérios de Aceitação:** O Administrador deve conseguir editar o valor da cobrança, valendo para o próximo ciclo de faturamento.

---

**[RF11] Auditoria de Acesso e Segurança**: Como Administrador, quero garantir que o acesso ao sistema administrativo seja seguro e que os laudos dos pacientes não sejam expostos. 

**Fluxo Principal:**
1. Administrador realiza login com autenticação de dois fatores (2FA).
2. O sistema mascara dados sensíveis de pacientes nas listagens gerais.
3. O sistema impede que o Administrador visualize ou faça download dos arquivos de laudo enviados pelas clínicas. 


---


1. **Isolamento de Arquivos:** Os laudos (PDFs/Imagens) devem ser armazenados em uma pasta (Bucket) onde a chave de acesso é gerada apenas para o CPF do paciente ou para o usuário da clínica. O Admin da plataforma não deve ter essa chave "na mão".
    
2. **MFA Obrigatório:** Como o Admin tem "poder total" sobre as clínicas, o login dele **precisa** de um segundo fator de autenticação (como um código no celular). Se a senha vazar, o sistema continua protegido.
    
3. **Logs de Atividade:** Crie uma tabela simples no banco de dados chamada `logs_atividades`. Toda vez que o admin mudar um preço ou deletar um comentário, o sistema grava: `[Data] - [Admin] - [Ação]`. Isso desencoraja má conduta e ajuda a rastrear erros humanos.