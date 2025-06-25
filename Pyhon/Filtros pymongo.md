
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
			{"idade": 
				{"$lt": 20}}, {"idade": {"$gt": 60}}]})
```

Essa consulta está procurando documentos em que:

- **idade seja menor que 20** (`$lt` → _less than_)  
    **OU**
    
- **idade seja maior que 60** (`$gt` → _greater than_)
---

## ✅ 5. **Projeções (Selecionar Campos)**

```python
colecao.find({}, {"nome": 1, "email": 1, "_id": 0})
```

- Mostra só os campos `nome` e `email`, e **esconde o `_id`**.
    

---

## ✅ 6. **Ordenação**

```python
from pymongo import ASCENDING, DESCENDING

colecao.find().sort("idade", ASCENDING)
colecao.find().sort("data_criacao", DESCENDING)
```

---

## ✅ 7. **Limitar e Pular Documentos (Paginação)**

```python
colecao.find().skip(10).limit(5)
```

- Pula os 10 primeiros e retorna os próximos 5.
    

---

## ✅ 8. **Consultas com Expressões Regulares**

```python
colecao.find({"nome": {"$regex": "^A", "$options": "i"}})
```

- Retorna nomes que começam com "A", **ignorando maiúsculas/minúsculas**.
    

---

## ✅ 9. **Consultas em Campos Aninhados (Embedded Documents)**

```python
colecao.find({"endereco.cidade": "Quixadá"})
```

- Acessa diretamente subcampos.
    

---

## ✅ 10. **Consultas em Arrays**

```python
colecao.find({"tags": "urgente"})  # array contém o valor
colecao.find({"notas": {"$size": 3}})  # array com tamanho 3
colecao.find({"notas": {"$all": [10, 9]}})  # contém todos os valores
```

---

## ✅ 11. **Contar Documentos**

```python
colecao.count_documents({"ativo": True})
```

---

## ✅ 12. **Agregações (pipeline avançado)**

```python
pipeline = [
    {"$match": {"ativo": True}},
    {"$group": {"_id": "$idade", "total": {"$sum": 1}}},
    {"$sort": {"total": -1}}
]

resultados = list(colecao.aggregate(pipeline))
```

---

## ✅ 13. **Índices (Melhora performance)**

```python
colecao.create_index("email", unique=True)
colecao.create_index([("nome", ASCENDING), ("idade", DESCENDING)])
```

---

## ✅ 14. **Buscar por `_id`**

```python
from bson import ObjectId

colecao.find_one({"_id": ObjectId("665fe0b5f88c1f2c296d3dbf")})
```

> ⚠️ Sempre use `ObjectId()` para consultas com `_id`!

---

## ✅ 15. **Outras funções úteis**

```python
colecao.find_one_and_update()
colecao.find_one_and_delete()
colecao.find_one_and_replace()
```

---

## ✅ Dica: Transformar cursor em lista

```python
dados = list(colecao.find())
```

---

Se quiser, posso te dar **exemplos práticos** para cada item acima ou te ajudar a criar **um serviço com filtros dinâmicos** no FastAPI usando essas consultas. Quer seguir por algum deles?