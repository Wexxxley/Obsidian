
---

Assim como o Entity Framework Core é um **ORM (Object-Relational Mapper)**, para o MongoDB usamos algo similar: um **ODM (Object-Document Mapper)**.

No ecossistema .NET, a ferramenta que cumpre o papel de ODM para o MongoDB é o **Driver Oficial do MongoDB para .NET**, o pacote `MongoDB.Driver` que você já instalou.

Diferente de outros ecossistemas onde o driver de conexão e o ODM podem ser pacotes separados, no .NET, o driver oficial já vem com todas as funcionalidades de um ODM poderoso. Ele é a sua ponte completa para o banco de dados.

### O que o Driver do MongoDB faz por você (como um ODM)?

Ele oferece funcionalidades muito parecidas com as que você espera de um ORM como o EF Core:

1. **Mapeamento Objeto-Documento:**
    
    - Ele converte ("serializa") seus objetos C# (como a classe `Book`) em documentos BSON para serem salvos no MongoDB.
        
    - Ele converte os documentos BSON do banco de dados de volta ("desserializa") para objetos C# quando você faz uma consulta.
        
    - Ele usa convenções (como mapear uma propriedade `Id` para o campo `_id`) e atributos (como `[BsonId]`, `[BsonElement]`) para controlar esse mapeamento, assim como o EF Core faz.
        
2. **Abstração de Consultas (Queries):**
    
    - **Suporte a LINQ:** Assim como no EF Core, você pode escrever consultas usando LINQ, o que é extremamente poderoso e familiar.
        
        C#
        
        ```
        var livrosBaratos = await _booksCollection.AsQueryable()
                                                  .Where(b => b.Price < 50.00m)
                                                  .ToListAsync();
        ```
        
    - **Builders (API Fluente):** Ele também oferece uma API de construção de consultas (Builders) que é muito expressiva e otimizada para as funcionalidades do MongoDB.
        
        C#
        
        ```
        var filter = Builders<Book>.Filter.Eq(b => b.Author, "Machado de Assis");
        var livrosDoAutor = await _booksCollection.Find(filter).ToListAsync();
        ```
        
3. **Execução de Comandos CRUD:**
    
    - Ele fornece métodos diretos para criar, ler, atualizar e deletar documentos, como `InsertOneAsync`, `UpdateOneAsync`, `DeleteOneAsync`, `FindAsync`, etc.
        
    - **Diferença importante:** Enquanto o EF Core geralmente usa o padrão "Unit of Work" (você faz várias alterações e depois chama `SaveChanges()` para persistir tudo), no MongoDB, os comandos como `InsertOneAsync` são executados imediatamente no banco de dados.

### **1. Criando a primeira entidade**

Vou utilizar o MongoDB, então é preciso instalar o seguinte pacote.
![](attachments/Pasted%20image%2020250805102120.png)
![500](attachments/Pasted%20image%2020250805102557.png)