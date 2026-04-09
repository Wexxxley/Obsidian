
---


A ideia é basicamente ter um app que sirva como como intermediário entre o paciente e a clínica, clínicas essas que podem ofercer exames ou consults.
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

Sugestao
**Sistema de "Check-in Antecipado" e Triagem Digital:**

- **Inovação:** Em vez de apenas redirecionar para o WhatsApp, o app permite que o paciente anexe fotos de documentos (RG, Carteira do Convênio) e preencha uma pré-anamnese.
    
- **Valor:** Quando o paciente chega à clínica, a recepção já tem os dados prontos no sistema, reduzindo o tempo de espera na recepção — uma das maiores queixas em serviços de saúde.



**O que precisamos fazer:** 

- **Formação da Equipe:** Inicia-se com a definição de papéis complementares, sugerindo perfis como Visionário, Comunicador, Construtor, Gestor e Designer para garantir diversidade de habilidades em grupos de até 7 integrantes.
		- Wesley: Gestor
		- Pedro Arthur: Comunicador
		- Vinicius: Construtor
		- Kauã: Construtor
    
- **Diagnóstico do Problema:** Através da Árvore de Problemas

- **Estruturação do Valor:** Utiliza-se o **Canvas da Proposta de Valor** para alinhar as tarefas e dores do cliente aos produtos e aliviadores de dor da startup.
    
- **Modelo de Negócio (BMC):** É a etapa crítica onde a sustentabilidade financeira é desenhada nos 9 blocos do Business Model Canvas. É aqui que se inicia a avaliação quantitativa (notas) da disciplina.



