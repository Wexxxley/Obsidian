
---
ORM (Object Relational Mapping) é uma camada que permite conectar a programação orientada a objetos com bancos de dados relacionais, abstraindo os comandos SQL subjacentes. Vamos utilizar o ORM SqlModel.
## **1.1 Principais recursos**
- O ORM permite mapear classes e modelos de forma a realizar operações no banco de dados. 
- O ORM traduz automaticamente as instruções SQL para refletir as mudanças no banco de dados, e transforma os dados recuperados do banco em objetos.

![[Pasted image 20250522154928.png]]
1. **Engine**: O motor de conexão com o banco de dados
2. **create_db_and_tables:** função para criar as tabelas pelo primeira vez (chamada na main)

---
## **1.2 Criando modelos**

**Relacionamento 1:N**
![[Pasted image 20250522155121.png]]
![[Pasted image 20250522155137.png]]
Modelo de user
![[Pasted image 20250522155314.png]]

Na main é criado o banco ao iniciar, mas so pe criado a tabela um vez, mesmo que a aplicação seja recarregada.
![[Pasted image 20250522154841.png]]


