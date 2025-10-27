

---

O objetivo dos testes de integração é exercitar um **serviço completo** ou uma **funcionalidade de maior granularidade** do sistema. Eles verificam se diferentes partes do sistema (múltiplas classes, possivelmente de pacotes distintos) **funcionam juntas corretamente**.

**Características:**

- **Envolvem Múltiplas Classes:** Diferente dos testes de unidade, os testes de integração tipicamente interagem com várias classes ao mesmo tempo.
    
- **Usam Dependências Reais:** Ao contrário dos testes de unidade (onde usamos mocks/stubs para isolar), os testes de integração geralmente interagem com **dependências e sistemas reais**, como bancos de dados, serviços de rede externos, sistemas de arquivos, etc.. Mocks e stubs não são usados neste nível.
    
- **Mais Lentos:** Por envolverem mais código e interagirem com sistemas externos (disco, rede), eles executam mais lentamente que os testes de unidade.
    
- **Menos Frequentes:** Devido ao tempo de execução maior, são executados com menos frequência que os testes de unidade (ex: após cada commit para o servidor de CI, ou algumas vezes ao dia).
    

**Exemplo: Agenda de Compromissos**

- O livro usa o exemplo de uma Agenda de Compromissos com uma interface gráfica simples.
    
- Existe uma classe `AgendaFacade` que oferece métodos para adicionar (`addAppointment`), remover (`removeAppointment`) e listar (`listAppointments`) compromissos, interagindo com um banco de dados (`DB`) .
    
- Um teste de integração para `AgendaFacade` seria:
    
    Java
    
    ```
     @Test
     void AgendaFacadeTest() {
      // 1. Setup com dependência REAL (Banco de Dados)
      DB db = DB.create(); // Cria/conecta a um BD real (ex: em memória ou de teste)
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
    
      // 4. Assert: Verifica o resultado que dependeu da integração com o BD
      assertEquals(3, apps.length);
     }
    ```
    
- **Observações sobre o Exemplo:**
    
    - O teste ainda usa JUnit, mostrando que o framework serve para ambos os tipos de teste .
        
    - É classificado como de integração porque usa uma dependência real (o banco de dados `db`) em vez de um mock .
        
    - Ele exercita os principais serviços (`add`, `list`) e sua interação com a camada de persistência, mas **não testa a interface gráfica**. Por isso, ainda não é um teste de sistema completo (ponta-a-ponta).
        

Testes de integração são cruciais para garantir que as diferentes partes do sistema colaboram como esperado, especialmente em pontos onde há interação com infraestrutura externa.

Terminamos os Testes de Integração. Digite "next" para subirmos ao topo da pirâmide com os Testes de Sistema.