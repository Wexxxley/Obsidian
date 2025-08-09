
---
Assim como o Entity Framework Core é um **ORM (Object-Relational Mapper)**, para o MongoDB usamos algo similar: um **ODM (Object-Document Mapper)**.

No ecossistema .NET, a ferramenta que cumpre o papel de ODM para o MongoDB é o Driver Oficial do MongoDB para .NET, o pacote `MongoDB.Driver`.

**O que o Driver do MongoDB faz?**
1. **Mapeamento Objeto-Documento:**
    - Ele converte seus objetos C# em documentos BSON.
    - Ele converte os documentos BSON do banco de dados de volta para objetos C#.
    - Ele mapeia uma propriedade `Id` para o campo `_id`.
2. **Abstração de Consultas (Queries):**
    - **Suporte a LINQ:** Assim como no EF Core, você pode escrever consultas usando LINQ, o que é extremamente poderoso e familiar.
    - **Builders:** Ele também oferece uma API de construção de consultas (Builders) que é muito expressiva e otimizada para as funcionalidades do MongoDB.
3. **Execução de Comandos CRUD:**
    - Ele fornece métodos diretos para criar, ler, atualizar e deletar documentos, como `InsertOneAsync`, `UpdateOneAsync`, `DeleteOneAsync`, `FindAsync`, etc.
    - Enquanto o EF  usa o padrão "Unit of Work" (você faz várias alterações e depois chama `SaveChanges()`), no MongoDB, os comandos são executados imediatamente no db.

### **1. Criando a primeira entidade**

Vou utilizar o MongoDB, então é preciso instalar o seguinte pacote.

![](attachments/Pasted%20image%2020250805102120.png)

![500](attachments/Pasted%20image%2020250805102557.png)

