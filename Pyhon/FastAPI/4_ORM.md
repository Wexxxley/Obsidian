
---
ORM (Object Relational Mapping) é uma camada que permite conectar a programação orientada a objetos com bancos de dados relacionais, abstraindo os comandos SQL subjacentes.
## **1.1 Principais recursos**
- O ORM permite mapear classes e modelos de forma a realizar operações no banco de dados. 
- O ORM traduz automaticamente as instruções SQL para refletir as mudanças no banco de 
- dados, e transforma os dados recuperados do banco em objetos.

![[Pasted image 20250522104031.png]]
1. **Engine**: O motor de conexão com o banco de dados
	- `connection_string`  
	    Define o tipo do banco
	- `connect_args`  
	    `{"check_same_thread": False}`
	    - O SQLite, por padrão, não permite acessar a mesma conexão em diferentes threads.
2. **Session**: A sessão de comunicação com o banco. Ela representa uma **conversa temporária com o banco de dados**.
	- `autocommit=False`: Você precisa chamar `session.commit()` manualmente para salvar as alterações.
	- `autoflush=False`: Impede que a sessão envie automaticamente as mudanças para o banco antes de uma consulta.
	- `bind=engine`: Liga a sessão à engine, ou seja, define com qual banco ela vai se comunicar.
3. Base: É a **classe base de onde todas as suas classes de modelo vão herdar**.

---
## **1.2 Criando modelos**
![[Pasted image 20250522071219.png]]

Na main 
![[Pasted image 20250522101711.png]]