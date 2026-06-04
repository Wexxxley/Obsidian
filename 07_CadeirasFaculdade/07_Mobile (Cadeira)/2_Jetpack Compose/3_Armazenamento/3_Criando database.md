
#Concluded 

---
### **1. Entities**

- **@Entity**: Define que a classe é uma tabela. Podemos dar um nome a ela com tableName.
- **@PrimaryKey**: Toda tabela precisa de uma chave primária única. Usamos autoGenerate = true para o Room cuidar dos números (1, 2, 3...) para nós.
- **@ColumnInfo**: Define o nome da coluna no SQLite. Se não usar, o Room usa o nome da variável, mas é boa prática definir nomes claros.
- **ID 0**: definir o ID inicial como 0 sinaliza ao Room que ele deve gerar um novo número automaticamente.
![](../../../../attachments/Pasted%20image%2020260331071932.png)

---
### **2. DAO**

O DAO é uma interface anotada com @Dao. Você apenas define a assinatura dos métodos e o Room gera a implementação SQL em tempo de compilação.

Nunca faça operações de banco de dados na Main Thread.
- **suspend**: Faz com que o Kotlin saiba que essa função pode demorar e deve ser executada em uma Coroutine sem travar a tela.
- **OnConflictStrategy**: A estratégia **REPLACE** diz ao Room: Se já existir, substitua pela nova.

Para buscas personalizadas, usamos a anotação **@Query**.
- **`Flow<List<Note>>`**: Ao retornar um Flow, o Room se torna "reativo". Se você adicionar uma nota nova no banco, o Flow emitirá automaticamente uma nova lista atualizada para a sua UI, sem que você precise fazer uma nova consulta manual.

![530](../../../../attachments/Pasted%20image%2020260331090218.png)

---
### **3. Database**

A classe Database é o ponto central que conecta as tabelas aos seus comandos DAOs.

O **padrão Singleton** garante que uma classe tenha apenas uma instância durante toda a vida útil do app. Usamos o **applicationContext** em vez do contexto Activity para evitar vazamentos de memória. 

Como seu app pode tentar acessar o banco de dados de vários lugares ao mesmo tempo:

- **`@Volatile`**: Garante que o valor da variável seja lido diretamente da RAM e não do cache do processador. Isso faz com que, se uma Thread mudar o valor, todas as outras vejam a mudança instantaneamente.
- **`synchronized`**: Bloqueia a entrada de duas Threads simultâneas. 

![500](../../../../attachments/Pasted%20image%2020260331090539.png)
1. **@Database**: Informa ao Room que esta é a classe principal.
2. **RoomDatabase()**: Torna a classe uma infraestrutura oficial do Room.
3. **Método do DAO**: O Room implementará o código para você acessar o NoteDao.
4. **Companion Object**: Permite que você chame `NoteDatabase.getDatabase(context)` de qualquer lugar do app sem precisar instanciar a classe manualmente.
 
---
### **4. Repository**

O Repository é uma camada de abstração que atua como um mediador entre as fontes de dados (Banco de Dados Room, APIs externas, Cache). Embora não seja obrigatório, o Google o recomenda como uma boa prática de arquitetura.

O repositório recebe o DAO via construtor. O repositório só tem acesso aos comandos que ele realmente precisa usar.

- **suspend**: Uma função suspensa garante que ela pode ser pausada e retomada, permitindo que o Room execute a tarefa em background sem travar o app. Essencial em todas as funções de escrita/leitura (exceto no Flow).

![](../../../../attachments/Pasted%20image%2020260331091702.png)