
---

É do tipo **Document Databases**.

![[Pasted image 20250625140144.png]]

![[Pasted image 20250625140158.png]]

![[Pasted image 20250625140503.png]]
1. **`.model_dump()`**
    - Substitui `.dict()` por `.model_dump()`, que é o método recomendado nas versões recentes do Pydantic.
2. **Função utilitária `mongo_to_dict`**
    
    - Centraliza a conversão do `_id` para `id` e a remoção do campo `_id`.
    - Evita repetição de código e facilita manutenção.
3. **List comprehension na listagem**
    
    - Torna o código mais limpo e Pythonic ao converter todos os documentos de uma vez.
4. **`new_todo = todo.dict()`**
    
    - Converte o objeto recebido do tipo [Todo](vscode-file://vscode-app/c:/Users/Wesley%20Freitas/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html) (um Pydantic model) em um dicionário Python.
    - Isso facilita a inserção no MongoDB, pois o PyMongo espera um dicionário.
5. **`resultado = colecao.insert_one(new_todo)`**
    
    - Insere o novo documento na coleção do MongoDB.
    - O método retorna um objeto que contém, entre outras coisas, o [inserted_id](vscode-file://vscode-app/c:/Users/Wesley%20Freitas/AppData/Local/Programs/Microsoft%20VS%20Code/resources/app/out/vs/code/electron-sandbox/workbench/workbench.html), que é o `_id` gerado automaticamente pelo MongoDB para o novo documento.
6. **`created_todo = colecao.find_one({"_id": resultado.inserted_id})`**
    
    - Busca o documento recém-criado usando o `_id` retornado na inserção.
    - Isso garante que você está pegando exatamente o documento salvo, inclusive com o campo `_id` preenchido.
7. **`created_todo["id"] = str(created_todo["_id"])`**
    
    - Cria um novo campo chamado `id` no dicionário, convertendo o valor de `_id` (que é um `ObjectId`) para string.
    - Isso é necessário porque o tipo `ObjectId` não é serializável em JSON, mas a string é.
8. **`del created_todo["_id"]`**
    
    - Remove o campo original `_id` do dicionário.
    - Isso evita que o `ObjectId` seja retornado na resposta, o que causaria erro de serialização.
9. **`return created_todo`**
    
    - Retorna o dicionário já pronto para ser convertido em JSON pelo FastAPI.
    - Agora, todos os campos são serializáveis, então não haverá erro.