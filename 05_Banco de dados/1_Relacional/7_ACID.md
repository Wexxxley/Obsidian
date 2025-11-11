

---

ACID é um acrônimo que descreve as quatro propriedades essenciais de uma **transação de banco de dados confiável**. Essas propriedades garantem que, mesmo em caso de falhas, os dados permaneçam em um estado consistente.

- **A**tomicity (Atomicidade)
    
- **C**onsistency (Consistência)
    
- **I**solation (Isolamento)
    
- **D**urability (Durabilidade)

Condifere essa tabela como exemplo.
```sql
CREATE TABLE Contas (
    ContaID INT PRIMARY KEY,
    Titular VARCHAR(100),
    Saldo DECIMAL(10, 2)
);

INSERT INTO Contas (ContaID, Titular, Saldo) VALUES (1, 'Alice', 1000.00);
INSERT INTO Contas (ContaID, Titular, Saldo) VALUES (2, 'Beto', 500.00);
```

A transação é "transferir R$ 100 da Alice para o Beto". Isso envolve dois comandos: 
1. UPDATE para debitar
2. UPDATE para creditar.

---
### **A - Atomicidade**
Ou todas as operações da transação são concluídas com sucesso, ou nenhuma delas é. 

Cenário de Sucesso (COMMIT)

O SQL executa tudo dentro do `BEGIN` e, se chegar ao `COMMIT` sem erros, torna as mudanças permanentes.

SQL

```
BEGIN TRANSACTION; -- Abre o "envelope"

-- 1. Debitar da Alice
UPDATE Contas SET Saldo = Saldo - 100.00 WHERE ContaID = 1;

-- 2. Creditar ao Beto
UPDATE Contas SET Saldo = Saldo + 100.00 WHERE ContaID = 2;

COMMIT; -- Fecha o "envelope" e confirma TUDO.
```

**Resultado:** Alice = 900, Beto = 600. Perfeito.

#### Cenário de Falha (ROLLBACK)

E se o segundo `UPDATE` falhar? (Por exemplo, a `ContaID` 2 não existe).

SQL

```
BEGIN TRANSACTION;

-- 1. Debitar da Alice (Funciona!)
UPDATE Contas SET Saldo = Saldo - 100.00 WHERE ContaID = 1;

-- 2. Creditar ao Beto (Falha! A conta 999 não existe)
UPDATE Contas SET Saldo = Saldo + 100.00 WHERE ContaID = 999;
-- O banco de dados gera um ERRO AQUI.

ROLLBACK; -- O "envelope" é desfeito.
```

**O que a Atomicidade faz:** Como a transação terminou com `ROLLBACK` (ou um erro que o força), o banco **desfaz** a Operação 1. O saldo de Alice **volta** a ser 1000. O dinheiro não "desaparece no limbo". Isso é "Tudo ou Nada".
---

### 🛡️ Consistência (Consistency)

**"Mantenha as regras."**

A consistência garante que qualquer transação levará o banco de dados de um **estado válido** para outro **estado válido**. A transação não pode violar as regras de integridade do banco (como _constraints_, _triggers_ ou _foreign keys_).

- **Exemplo Prático (Saldo Negativo):** Se o banco de dados tem uma regra (uma _constraint_) que diz "o saldo de uma conta não pode ser negativo", a propriedade de Consistência impede qualquer transação que tente sacar mais dinheiro do que existe. A transação falhará e será revertida, mantendo o banco de dados em um estado válido.
    

---

### izolamento (Isolation)

**"Não se metam uns com os outros."**

O isolamento garante que transações que estão sendo executadas ao mesmo tempo (concorrentemente) não interfiram umas nas outras. Do ponto de vista de uma transação, deve parecer que ela é a **única** coisa sendo executada no banco de dados naquele momento.

- **Exemplo Prático (Relatório vs. Pagamento):**
    
    - **Transação A:** Está rodando um relatório que soma o saldo de todas as contas.
        
    - **Transação B:** Está processando um pagamento (tirando dinheiro de uma conta).
        
- **O que o Isolamento garante:** A Transação A (o relatório) não verá um "estado fantasma" onde o dinheiro já saiu da conta, mas o total do relatório ainda não foi atualizado. Ela verá o estado do banco _antes_ da Transação B começar ou _depois_ que ela terminar, mas nunca um estado inconsistente no meio do caminho.
    

---

### 💾 Durabilidade (Durability)

**"Uma vez salvo, salvo para sempre."**

A durabilidade garante que, uma vez que uma transação tenha sido **confirmada** (commit), ela é **permanente**. As mudanças sobreviverão a qualquer falha subsequente do sistema, como uma queda de energia ou uma falha do servidor.

- **Exemplo Prático (Confirmação de Compra):** Quando você recebe a mensagem "Pagamento Aprovado", a durabilidade garante que essa transação foi registrada em um armazenamento não volátil (como um log de transações em um SSD/HD). Mesmo que o servidor do banco de dados caia um segundo depois, sua compra não será "esquecida". Quando o sistema voltar, a transação estará lá, completa.













---



---

### C - Consistência (Manter as Regras)

A consistência garante que o banco de dados só pode ir de um **estado válido** para outro **estado válido**. O banco de dados **impõe as regras** que você define.

**Como o SQL faz isso:** Através de `CONSTRAINTS` (restrições) como `NOT NULL`, `UNIQUE`, `FOREIGN KEY` e, o mais importante aqui, `CHECK`.

#### Cenário de Falha (Violação de Regra)

Vamos adicionar uma regra de negócio: "o saldo nunca pode ficar negativo".

SQL

```
-- Adicionando uma regra (CONSTRAINT) na tabela
ALTER TABLE Contas
ADD CONSTRAINT CHK_SaldoPositivo CHECK (Saldo >= 0);
```

Agora, vamos tentar fazer uma transação que viole essa regra: Alice (que tem 1000) tenta transferir 1500 para o Beto.

SQL

```
BEGIN TRANSACTION;

-- 1. Debitar da Alice (1000 - 1500 = -500)
UPDATE Contas SET Saldo = Saldo - 1500.00 WHERE ContaID = 1;
-- ERRO! A CONSTRAINT CHK_SaldoPositivo é violada AQUI.

-- 2. O comando abaixo nem chega a ser executado
UPDATE Contas SET Saldo = Saldo + 1500.00 WHERE ContaID = 2;

ROLLBACK;
```

**O que a Consistência faz:** O banco de dados nem sequer _permite_ que o primeiro `UPDATE` seja concluído. Ele falha imediatamente porque a regra `CHECK (Saldo >= 0)` seria quebrada. O banco se recusa a entrar em um estado "inválido". A Atomicidade (acima) então garante que a transação inteira seja desfeita.

---

### I - Isolamento (Não se Metam uns com os Outros)

O isolamento garante que transações concorrentes (acontecendo ao mesmo tempo) não interfiram umas nas outras. Do ponto de vista de uma transação, parece que ela está sendo executada sozinha no banco.

**Como o SQL faz isso:** Através de **mecanismos de travamento (Locking)**.

#### Cenário de Falha (Leitura Suja - Dirty Read)

Imagine que a nossa transferência (Alice -> Beto) está demorando. Ao mesmo tempo, um "Relatório" tenta somar todo o dinheiro do banco.

|**Tempo**|**Transação 1 (Transferência)**|**Transação 2 (Relatório)**|**Saldo (Alice/Beto)**|**Total**|
|---|---|---|---|---|
|T1|`BEGIN TRANSACTION;`||1000 / 500|1500|
|T2|`UPDATE Contas SET Saldo = 900 WHERE ContaID = 1;`||900 / 500|1400|
|T3||`SELECT SUM(Saldo) FROM Contas;`|||
|T4|`UPDATE Contas SET Saldo = 600 WHERE ContaID = 2;`||900 / 600|1500|
|T5|`COMMIT;`||900 / 600|1500|

**O que o Isolamento faz:** No T3, o que o Relatório deve ler?

- **Sem Isolamento:** O Relatório leria `900 + 500 = 1400`. Ele leria os dados "sujos" (meio-feitos) da Transação 1. O total do banco pareceria R$ 100 mais pobre!
    
- **Com Isolamento:** O banco de dados "trava" (coloca um _lock_) as linhas que a Transação 1 está modificando. Quando o Relatório (Transação 2) tenta ler no T3, o banco de dados o faz **esperar**. Somente após o `COMMIT` no T5 é que o banco libera o _lock_, e o Relatório pode ler o estado _novo e consistente_ (`900 + 600 = 1500`).
    

---

### D - Durabilidade (Salvo para Sempre)

A durabilidade garante que, uma vez que a transação recebe o `COMMIT`, as mudanças são **permanentes** e sobreviverão a qualquer falha (queda de energia, crash do servidor).

**Como o SQL faz isso:** Através do **Transaction Log (Log de Transações)**, também conhecido como Write-Ahead Log (WAL).

Isto não é um comando SQL, mas sim como o motor do banco funciona "por baixo dos panos".

#### Cenário de Falha (Queda de Energia)

1. Você executa: `COMMIT;`
    
2. O banco de dados **não** reescreve imediatamente os arquivos principais da tabela (que são grandes e lentos de modificar).
    
3. Em vez disso, ele **rapidamente** escreve a mudança (ex: "Conta 1, Saldo agora é 900") em um arquivo de log sequencial (o **Transaction Log**), que é muito rápido.
    
4. Assim que o _log_ é salvo no disco, o banco te responde "OK, comitado!".
    
5. ... (Processos em segundo plano atualizam os arquivos principais depois) ...
    
6. **O SERVIDOR CAI! (Queda de energia)**
    

**O que a Durabilidade faz:** Quando o servidor religar, antes de qualquer coisa, ele vai ler o **Transaction Log**. Ele verá: "Opa, a transação para `ContaID=1, Saldo=900` foi _comitada_, mas o servidor caiu antes que eu pudesse salvar no arquivo principal". O banco então usa esse log para **refazer** (roll forward) a operação e garantir que o saldo de Alice seja 900, como prometido. O `COMMIT` é uma promessa que não pode ser quebrada.