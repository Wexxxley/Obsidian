
---


---
### **1. Filtros**

Os métodos como **find_one, updated_one e delete_one** recebem um **filtro** como argumento. Esse filtro é um dicionário Python que define os critérios de busca para selecionar os documentos que você quer manipular.

No exemplo: **colecao.delete_one({"_id": ObjectId(id)})**
- O filtro diz:  "Procure um documento cujo campo `_id` seja igual ao id"
- O filtro é sempre um dicionário, onde as chaves são os nomes dos campos do documento e os valores são os critérios de busca.

---

### **2. Consulta Simples**
```python
colecao.find_one({"nome": "João"})
```
- Retorna **apenas o primeiro documento** que corresponde ao filtro.

```python
colecao.find({"idade": 30})
```
- Retorna **um cursor com todos os documentos** com idade = 30.

---
### **3. Iterando os Resultados**
```python
for documento in colecao.find({"ativo": True}):
    print(documento)
```

---
###  **3. Operadores de Comparação**

| Operador | Descrição             | Exemplo                         |
| -------- | --------------------- | ------------------------------- |
| `$eq`    | Igual a               | `{"idade": {"$eq": 25}}`        |
| `$ne`    | Diferente de          | `{"idade": {"$ne": 25}}`        |
| `$gt`    | Maior que             | `{"idade": {"$gt": 18}}`        |
| `$gte`   | Maior ou igual a      | `{"idade": {"$gte": 18}}`       |
| `$lt`    | Menor que             | `{"idade": {"$lt": 60}}`        |
| `$lte`   | Menor ou igual a      | `{"idade": {"$lte": 60}}`       |
| `$in`    | Está em uma lista     | `{"idade": {"$in": [25, 30]}}`  |
| `$nin`   | Não está em uma lista | `{"idade": {"$nin": [25, 30]}}` |

---
### **4. Operadores Lógicos**

`$and`, `$or`, `$not`, `$nor`

```python
colecao.find(
		{"$or": [
			{"idade": {"$lt": 20}},
			{"idade": {"$gt": 60}}]
		})
```
- Essa consulta está procurando documentos em que a idade seja menor que 20 OU idade seja maior que 60

---
### **5. Ordenação**
```python
from pymongo import ASCENDING, DESCENDING

colecao.find().sort("idade", ASCENDING)
colecao.find().sort("data_criacao", DESCENDING)
```

---
### **7. Paginação**

```python
colecao.find().skip(10).limit(5)
```
- Pula os 10 primeiros e retorna os próximos 5

---
### **8. Consultas em Campos Aninhados **
```python
colecao.find({"endereco.cidade": "Quixadá"})
```
- Acessa diretamente subcampos.

---
### **9. Contar Documentos**
```python
colecao.count_documents({"ativo": True})
```

---
### **10. Cursor**

Um **cursor** é um **objeto iterável** que representa o **resultado de uma consulta** no MongoDB. Quando você faz um `find()`, ele **não retorna diretamente uma lista de documentos**, mas sim um _cursor_ que **vai percorrendo os dados aos poucos**

```python
cursor = colecao.find({"ativo": True})

for documento in cursor:
    print(documento)
```
Aqui, `cursor` **não é uma lista**, mas sim algo que você pode **percorrer com `for`**.

- Se o banco tiver **milhares de documentos**, ele **não carrega tudo de uma vez**.
- Ele **busca sob demanda**, aos poucos — o que economiza **memória**.
- Perfeito para processar resultados grandes sem travar sua aplicação.

Cursor em lista.
```python
dados = list(colecao.find())
```
Se a coleção for **grande**, isso pode consumir muita memória.
