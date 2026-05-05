
#Concluded 

---
Uma consulta aninhada (ou subconsulta) é uma consulta `SELECT` que é executada _dentro_ de outra consulta SQL (a consulta externa). Ela é usada para buscar dados que servem como condição ou como um valor para a consulta principal.

### **1. Subconsulta Escalar**
Retorna exatamente um único valor (uma linha, uma coluna). 

**Exemplo:** Você quer listar todos os produtos que custam _acima da média_ de preços de todos os produtos.
```sql
SELECT Nome,Preco FROM Produtos
WHERE Preco > (
        SELECT AVG(Preco) FROM Produtos 
	  );
```

### **2. Subconsulta de Única Linha**
Retorna uma linha completa.

**Exemplo:** Você quer encontrar os dados do cliente que fez um pedido específico.
```sql
SELECT Nome,Cidade FROM Clientes
WHERE ClienteID = (
        SELECT ClienteID FROM Pedidos WHERE PedidoID = 101
      );
```

### **3. Subconsulta de Tabela**
Retorna um conjunto de resultados com várias linhas e várias colunas, como se fosse uma tabela temporária.

**Exemplo:** Você quer ver o nome de todos os clientes que moram no "Rio de Janeiro" e que também fizeram pedidos.

```sql
SELECT ClientesRJ.Nome, ClientesRJ.Cidade
FROM(
        SELECT ClienteID, Nome, Cidade
        FROM Clientes
        WHERE Cidade = 'Rio de Janeiro'
    ) AS ClientesRJ
JOIN Pedidos ON ClientesRJ.ClienteID = Pedidos.ClienteID;
```

---
### **4. ANY e SOME**

A condição é verdadeira se o valor da consulta externa for verdadeiro para pelo menos um dos valores retornados pela subconsulta.
    
**Exemplo:** Encontrar produtos que custam mais caro que qualquer produto da categoria 'Eletrônicos' (CategoriaID = 5).

```sql
SELECT Nome, Preco
FROM Produtos
WHERE Preco > ANY (
	SELECT Preco FROM Produtos WHERE CategoriaID = 5
);
-- Se 'Eletrônicos' tiver produtos de R$100, R$500 e R$1000,
-- este comando retornará produtos que custam mais que R$100.
```

---
### **4. ALL** 
A condição é verdadeira se o valor da consulta externa for verdadeiro para todos os valores retornados pela subconsulta.
    
**Exemplo:** Encontrar produtos que custam mais caro que _todos_ os produtos da categoria 'Eletrônicos'.

```sql
SELECT Nome, Preco
FROM Produtos
WHERE Preco > ALL (
	SELECT Preco FROM Produtos WHERE CategoriaID = 5
);
-- Usando o mesmo caso, este comando só retornará produtos que custam mais que R$1000.
```

---
### **5. EXISTS e NOT EXISTS**

Esses operadores não olham para os _valores_, mas apenas testam se a subconsulta retorna alguma linha ou não. 

**EXISTS:** A condição é verdadeira se a subconsulta retornar pelo menos uma linha.
    
**Exemplo:** Listar todos os clientes que já fizeram (existe) pelo menos um pedido.
```sql
SELECT
	Nome
FROM
	Clientes AS C
WHERE
	EXISTS (
		SELECT 1 -- O "1" é um truque, pode ser qualquer coisa
		FROM Pedidos AS P
		WHERE P.ClienteID = C.ClienteID 
	);
```
    
**NOT EXISTS:** A condição é verdadeira se a subconsulta não retornar nenhuma linha.
    
**Exemplo:** Listar todos os clientes que nunca (não existe) fizeram um pedido.
```sql
SELECT
	Nome
FROM
	Clientes AS C
WHERE
	NOT EXISTS (
		SELECT 1
		FROM Pedidos AS P
		WHERE P.ClienteID = C.ClienteID
	);
```

