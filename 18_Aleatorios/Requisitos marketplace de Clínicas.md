

---
- Consulta, exames (loboratorial e de imagem).
- O mvp não vai considerar Convênio.
- O cadastro de clinicas é feito pelos admins do sistema.
- Faz sentido ter os doutores individualmente.
- Cobrança individua para cada clinica.
- Pagamento de consulta/exame fica pela clinica
- Historico de resultados e consultas/exames (sugestão)

![300](../attachments/Screenshot_20260331_180610_Medclub.jpg)
![300](../attachments/Screenshot_20260331_180450_Medclub.jpg)
![](../attachments/Pasted%20image%2020260331181103.png)

## **Módulo do Paciente**
### **[RF01] Buscar Consultas e exames**

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

### **[RF02] Agendar Consulta/Exame**

**Descrição:** Como Paciente, quero selecionar um horário disponível na agenda de uma clínica para realizar o agendamento.

**Fluxo Principal:**
1. Usuário seleciona uma clínica/profissional.
2. Formulario para mensagem pronta.
3. Redirecionamento para o whatsapp/site.

### **[RF03] Feedback para a clínica**

**Descrição:** Como Paciente, quero poder dar um feedback da clínica

**Fluxo principal:**
1. Usários acessam o perfil da clinica
2. Opção de feedback

---
## **Módulo da Clínica**

### **[RF05] Edição de informações**

**Descrição**: Eu como profissional, gostaria de poder editar horarios, localização, descrição, profissionais, serviços, especialidades, foto.
### **[RF06] Upload de resultados/documentos (DADOS SENSÍVEIS)**

**Descrição**: Eu como profissional gostaria de fazer uploads de resultados por cpf.


---
## **Módulo Administrativo** 

### **[RF06] Credenciamento de Parceiros**

**Descrição:** Como Administrador, quero validar a documentação de novas clínicas para garantir a segurança da plataforma.

**Fluxo Principal:**
1. Administrador acessa "Solicitações de Cadastro".
2. Analisa o CNPJ, CRM/RQE do responsável.
3. Define o percentual de comissão
4. Aprova o cadastro.
    
**Fluxos Alternativos:**
- FA01: Documentação inválida (O sistema permite enviar uma notificação solicitando correção).
    
**Mensagens do Sistema:**
- MSG01: "Parceiro ativado com sucesso."
    
**Critérios de Aceitação:** A clínica só aparece nos resultados de busca após o status ser alterado para "Ativo".    

### **[RF07] Dashboard Financeiro e Repasse**

**Descrição:** Como Administrador, quero visualizar o volume total de transações e o status dos repasses financeiros.

**Fluxo Principal:**

1. Acessa "Relatórios Financeiros".
2. Filtra por período (Início e Fim).
3. Visualiza: Total Transacionado, Comissões Retidas e Valores a Repassar.
4. Exporta relatório em PDF/CSV.

---
## **Notificações** 
### **[RF08] Notificação Push e Lembretes**

**Descrição:** Como Sistema, quero enviar lembretes automáticos para reduzir o esquecimento.

**Fluxo Principal:**
1. O sistema identifica agendamentos para as próximas 24 horas.
2. Dispara notificação push/SMS para o Paciente.
3. Dispara lembrete para a Clínica