
---

É do tipo **Document Databases**.

### **1. Database**
![[Pasted image 20250625140144.png]]

---
### **2. Main**
![[Pasted image 20250625140158.png]]

---
### **3. Create**
![[Pasted image 20250625140503.png]]
4. **`.model_dump()`**: 
	- Converte para dicionario. Isso facilita a inserção no MongoDB, pois o PyMongo espera um dicionário.
5. **`resultado = colecao.insert_one(new_todo)`**
    - Insere o novo documento na coleção do MongoDB. O método retorna um objeto que contém, entre outras coisas, o inserted_id que é o `_id` gerado automaticamente.
6. **`created_todo = colecao.find_one({"_id": resultado.inserted_id})`**
    - Busca o documento recém-criado usando o `_id` retornado na inserção.
    - Isso garante que você está pegando o documento com o campo `_id`

![[Pasted image 20250625140942.png]]
1. **Função utilitária `mongo_to_dict`**
    - Cria um novo campo chamado `id` no dicionário, convertendo o valor de `_id` (que é um `ObjectId`) para string.
	- Isso é necessário porque o tipo `ObjectId` não é serializável em JSON, mas a string é.

---
### **4. Get_all**
![[Pasted image 20250625141249.png]]

---
### **5. Get por id** 
![[Pasted image 20250625141655.png]]
- ObjectId.is_valid(id): Garante que o id passado tem o formato correto antes de tentar converter, evitando exceções desnecessárias.
---
### **6. Update**

![[Pasted image 20250625142051.png]]
1. **Validação do id:**  
	- Antes de tentar atualizar, verifica se o tem o formato correto de um ObjectId do MongoDB. 
2. **Atualização do documento:**  
    - Tenta atualizar o documento cujo `_id` corresponde ao informado, usando os dados recebidos no corpo da requisição
3. **Verificação de existência:**  
    - Se nenhum documento foi encontrado para atualizar, retorna erro 404.

---
### **7. Delete**
![[Pasted image 20250625142501.png]]