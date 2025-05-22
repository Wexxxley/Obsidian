
---

**Alembic** é uma biblioteca Python que permite migrações de banco de dados controladas e automatizadas. Esta biblioteca utiliza ` SQLAlchemy`e permite o gerenciamento de alterações no esquema do banco de dados por meio de scripts, que descrevem as modificações e podem ser aplicadas automaticamente.

### 1. `alembic init alembic`

Cria a estrutura básica do Alembic no seu projeto:

- Um diretório `alembic/` com os arquivos de migração.
    
- Um arquivo `alembic.ini` com configurações (como string de conexão).
    
- Um `env.py`, que define como o Alembic interage com o SQLAlchemy.
    

---

### 🧠 2. `alembic revision -m "mensagem"`

Cria um **arquivo de migração vazio** com uma mensagem descritiva (ex: `"add users table"`).  
Esse arquivo será usado para definir alterações no schema.

---

### 🔍 3. `alembic revision --autogenerate -m "mensagem"`

Gera automaticamente uma **migração com base nas mudanças** detectadas no modelo SQLAlchemy comparado com o estado atual do banco.

Exemplo:

bash

CopiarEditar

`alembic revision --autogenerate -m "create todos table"`

⚠️ Você precisa garantir que o Alembic saiba onde está seu `Base` e engine, geralmente dentro do `env.py`.

---

### 🆙 4. `alembic upgrade head`

Aplica todas as migrações **pendentes** (do estado atual até o último "revision").

Outras opções:

- `upgrade +1` → aplica **uma** migração.
    
- `upgrade <revision_id>` → aplica até um ponto específico.
    

---

### ⬇️ 5. `alembic downgrade -1`

Desfaz a **última** migração aplicada.

Outras opções:

- `downgrade base` → volta ao estado inicial (nenhuma migração).
    
- `downgrade <revision_id>` → volta até uma migração específica.