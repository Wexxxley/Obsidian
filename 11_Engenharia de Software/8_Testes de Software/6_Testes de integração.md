
#Concluded 

---

O objetivo dos testes de integração é exercitar um serviço/funcionalidade completa do sistema. Eles verificam se diferentes partes do sistema (múltiplas classes, pacotes distintos) funcionam juntas corretamente.

**Características:**
- Envolvem Múltiplas Classes
- **Usam Dependências Reais:** Os testes de integração geralmente interagem com dependências e sistemas reais, como bancos de dados, serviços de rede externos, sistemas de arquivos, etc.. 
- **Menos Frequentes:** Devido ao tempo de execução maior, são executados com menos frequência que os testes de unidade (ex: após cada commit
    

**Exemplo: Agenda de Compromissos**
   
- Existe uma classe `AgendaFacade` que oferece métodos para adicionar (`addAppointment`), remover (`removeAppointment`) e listar (`listAppointments`) compromissos, interagindo com um banco de dados (`DB`) .
    
    ```java
     @Test
     void AgendaFacadeTest() {
      // 1. Setup com dependência REAL (Banco de Dados)
      DB db = DB.create(); // Cria/conecta a um BD real
      AgendaFacade agenda = new AgendaFacade(db);
    
      // 2. Cria objetos de negócio
      Appointment app1 = new Appointment(...);
      Appointment app2 = new Appointment(...);
      Appointment app3 = new Appointment(...);
    
      // 3. Executa as operações do serviço (que interagem com o BD)
      int id1 = agenda.addAppointment(app1);
      int id2 = agenda.addAppointment(app2);
      int id3 = agenda.addAppointment(app3);
      Appointment[] apps = agenda.listAppointments();
    
      // 4. Assert: Verifica o resultado 
      assertEquals(3, apps.length);
     }
    ```
    
- O teste ainda usa JUnit, mostrando que frameworks servem para ambos os tipos de teste .
- É classificado como de integração porque usa uma dependência real (o banco de dados `db`) em vez de um mock .
- Ele exercita os principais serviços (`add`, `list`) e sua interação com a camada de persistência, mas não testa a interface gráfica.

