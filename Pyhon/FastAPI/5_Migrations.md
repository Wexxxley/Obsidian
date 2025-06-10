
---

**Alembic** é uma biblioteca Python que permite migrações de banco de dados controladas e automatizadas. Esta biblioteca utiliza `SQLAlchemy`e permite o gerenciamento de alterações no esquema do banco de dados por meio de scripts, que descrevem as modificações e podem ser aplicadas automaticamente.
### **1. Principais comandos**
1. `alembic init alembic`: Cria a estrutura básica do Alembic no seu projeto:
- Um diretório `alembic/` com os arquivos de migração.
- Um arquivo `alembic.ini` com configurações (como string de conexão).

1. `alembic revision -m "mensagem"`: Cria um **arquivo de migração vazio**. Esse arquivo será usado para definir alterações no schema.
	 Em env.py é preciso importar seus modelos e definir o matadata alvo.
	![[Pasted image 20250523155642.png]]
	![[Pasted image 20250523155655.png]]
2. `alembic revision --autogenerate -m "mensagem"`: Gera automaticamente uma **migração com base nas mudanças** detectadas no modelo comparado com o estado atual do banco.
3. `alembic upgrade revision-id`: É como de fato fazemos a atualização do banco de dados.
4. `alembic downgrade -1`: faz o downgrade para a última migração.


Link para reposiório de exemplo: https://github.com/Wexxxley/01-MuscleFlowApi