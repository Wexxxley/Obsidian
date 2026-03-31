

---
- Consulta, exames (loboratorial e de imagem).
- O mvp não vai considerar Convênio.
- O cadastro de clinicas é feito pelos admins do sistema.
- Faz sentido ter os doutores individualmente.
- Cobrança individua para cada clinica.
- Pagamento de consulta/exame fica pela clinica


## **Módulo do Paciente**

### **[RF01] Cadastro e login**

Cpf, email, endereço, nome completo e telefone.
### **[RF02] Buscar Consultas e exames**

**Descrição:** Como Paciente, quero pesquisar por especialidades(dentista, oftamologista...), procedimentos ou nomes de clínicas para encontrar o atendimento necessário. Consulta e exame.

**Fluxo Principal:**
1. Usuário acessa a barra de busca na tela inicial.
2. Digita o termo de busca (ex: "Cardiologia" ou "Exame de Sangue").
3. O sistema utiliza a **geolocalização** para filtrar resultados próximos.
4. O sistema exibe uma lista de clínicas e distância.
    
**Fluxos Alternativos:**    
- FA01: Geolocalização desativada (O sistema solicita a inserção do CEP ou cidade).
    
**Mensagens do Sistema:**
- MSG01: "Nenhum prestador encontrado nesta região."
    
**Critérios de Aceitação:** A busca deve retornar os resultados podendo filtrar.

### **[RF03] Agendar Consulta/Exame**

**Descrição:** Como Paciente, quero selecionar um horário disponível na agenda de uma clínica para realizar o agendamento.

**Fluxo Principal:**
1. Usuário seleciona uma clínica/profissional.
2. Formulario para mensagem pronta.
3. Redirecionamento para o whatsapp/site.

### **[RF04] Acessar perfil da clinica**

**Descrição**: ifood de servicos e profissionais. Exame de sangue com o Dr.Drauzio.

### **[RF05] Feedback para a clínica**

**Descrição:** Como Paciente, quero poder dar um feedback da clínica

**Fluxo principal:**
1. Usários acessam o perfil da clinica
2. Opção de feedback


---
## **Módulo da Clínica**

### **[RF06] Edição de informações do "Perfil"**

**Descrição**: Eu como profissional, gostaria de poder editar horarios, localização, descrição, profissionais, serviços, especialidades, foto.

### **[RF07] Upload de resultados/documentos (DADOS SENSÍVEIS)**

**Descrição**: Eu como profissional gostaria de fazer uploads de resultados por cpf.

