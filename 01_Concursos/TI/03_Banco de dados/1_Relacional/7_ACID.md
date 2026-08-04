
#Concluded 

---

São propriedades essenciais de uma **transação de banco de dados confiável**: Atomicidade, Consistência, Isolamento, Durabilidade.

Considere essa tabela como exemplo.
```sql
CREATE TABLE Contas (
    ContaID INT PRIMARY KEY,
    Titular VARCHAR(100),
    Saldo DECIMAL(10, 2)
);

INSERT INTO Contas (ContaID, Titular, Saldo) VALUES (1, 'Alice', 1000.00);
INSERT INTO Contas (ContaID, Titular, Saldo) VALUES (2, 'Beto', 500.00);
```

A transação é "transferir 100 da Alice para o Beto". Isso envolve dois comandos: 
1. UPDATE para debitar
2. UPDATE para creditar.

---
### **1. Atomicidade**
Ou todas as operações da transação são concluídas, ou nenhuma delas é.

```sql
BEGIN -- 1. Tenta executar a lógica de negócio
    
    -- Debita da Alice
    UPDATE Contas SET Saldo = Saldo - 100.00 WHERE ContaID = 1;
    -- Credita ao Beto
    UPDATE Contas SET Saldo = Saldo + 100.00 WHERE ContaID = 2;
    
    commit;
    
EXCEPTION
    rollback;
END;

```
O SQL executa tudo dentro do `BEGIN` e, se chegar ao `COMMIT` sem erros, torna as mudanças permanentes.

---
### **2. Consistência**
A consistência garante que o banco de dados só pode ir de um estado válido para outro estado válido. O banco de dados **impõe regras** que você define. Através de `CONSTRAINTS`.

Vamos adicionar uma regra de negócio: "o saldo nunca pode ficar negativo".
```sql
ALTER TABLE Contas 
ADD CONSTRAINT CHK_SaldoPositivo CHECK (Saldo >= 0);
```

Agora, vamos tentar fazer uma transação que viole essa regra.
```sql
BEGIN;
	-- 1. Debitar da Alice (1000 - 1500 = -500)
	UPDATE Contas SET Saldo = Saldo - 1500.00 WHERE ContaID = 1;
	-- ERRO! A CONSTRAINT CHK_SaldoPositivo é violada AQUI.
	-- 2. O comando abaixo nem chega a ser executado
	UPDATE Contas SET Saldo = Saldo + 1500.00 WHERE ContaID = 2;
    commit;
    
EXCEPTION
    rollback;
END;
```

A recomendação arquitetural moderna defende a separação estrita de responsabilidades. O ideal não é a duplicação do código, mas a implementação de camadas complementares de segurança, um conceito conhecido como **Defesa em Profundidade (Defense in Depth).** 

- **O Papel da Camada de Aplicação:** A camada de aplicação deve centralizar a lógica de negócio e as regras de domínio. A validação de dados neste nível impede o envio de requisições inúteis.
	- **Ex:** validar se a idade de um cliente permite a contratação de um serviço específico.
- **O Papel do Banco de Dados:** O banco de dados atua como a última linha de defesa, garantindo a integridade relacional absoluta da informação. 
	- **Ex:** garantir, por meio de uma `FOREIGN KEY`, que um pedido de compra jamais seja associado a um identificador de cliente inexistente.
    
---
### **3. Isolamento**
O isolamento garante que transações concorrentes não interfiram umas nas outras. Imagine que a nossa transferência (Alice -> Beto) está demorando. Ao mesmo tempo, um "Relatório" tenta somar todo o dinheiro do banco.

|     | **Transferência**                                  | **Relatório**                    | **Saldo (Alice/Beto)** | **Total** |
| --- | -------------------------------------------------- | -------------------------------- | ---------------------- | --------- |
| T1  | `BEGIN TRANSACTION;`                               |                                  | 1000 / 500             | 1500      |
| T2  | `UPDATE Contas SET Saldo = 900 WHERE ContaID = 1;` |                                  | 900 / 500              | 1400      |
| T3  |                                                    | `SELECT SUM(Saldo) FROM Contas;` |                        |           |
| T4  | `UPDATE Contas SET Saldo = 600 WHERE ContaID = 2;` |                                  | 900 / 600              | 1500      |
| T5  | `COMMIT;`                                          |                                  | 900 / 600              | 1500      |

No T3, o que o Relatório deve ler?

- **Sem Isolamento:** O Relatório leria `900 + 500 = 1400`. Ele leria os dados 'meio feitos" da Transação 1. 
    
- **Com Isolamento:** O banco de dados "trava" (coloca um _lock_) as linhas que a Transação 1 está modificando. Quando o Relatório  tenta ler no T3, o banco de dados o faz esperar. Somente após o `COMMIT` no T5 é que o banco libera o _lock_, e o Relatório pode ler o estado _novo e consistente_ (`900 + 600 = 1500`).

---
### **D - Durabilidade**

<mark style="background: #ADCCFFA6;">A durabilidade garante que, uma vez que a transação recebe o COMMIT, as mudanças são permanentes e sobreviverão a qualquer falha.</mark>

1. Você executa: `COMMIT;`
    
2. O banco de dados não reescreve imediatamente os arquivos principais da tabela (que são grandes e lentos de modificar).
    
3. Em vez disso, ele rapidamente escreve a mudança no arquivo **Transaction Log**, que é muito rápido.
    
4. Assim que o _log_ é salvo no disco, o banco te responde "OK, comitado!".
    
5. Processos em segundo plano atualizam os arquivos principais depois
    
6. **O SERVIDOR CAI!**

Quando o servidor religar, antes de qualquer coisa, ele vai ler o **Transaction Log**. Ele verá: "Opa, a transação para `ContaID=1, Saldo=900` foi _comitada_, mas o servidor caiu antes que eu pudesse salvar no arquivo principal". O banco então usa esse log para refazer a operação e garantir que o saldo de Alice seja 900, como prometido. 


