
#Concluded 

---
![550](attachments/Pasted%20image%2020250809073302.png)
1. `Find(filter)`: Ele não executa a busca no banco de dados imediatamente; em vez disso, ele **prepara a consulta** com base em um filtro que você fornece.
    - `Find(_ => true)`: O `_ => true` é um filtro que significa "retorne verdadeiro para todos os documentos". 
    - `Find(b => b.Id == id)`: Aqui, o filtro é uma expressão lambda que busca por um documento onde a propriedade `Id` seja igual ao `id` fornecido. 
2. `ToListAsync()`: Executa a consulta preparada pelo`Find` e retorna **todos os documentos** que correspondem ao filtro em uma lista (`List<T>`).
![550](attachments/Pasted%20image%2020250809073544.png)
3. `FirstOrDefaultAsync()`:Assim como o `ToListAsync`, ele **executa a consulta** do `Find`. No entanto, ele para assim que encontra o **primeiro documento** que corresponde ao filtro.
4. `InsertOneAsync(document)`:Ele insere **um único documento** na coleção.
![600](attachments/Pasted%20image%2020250809073734.png)
5. `ReplaceOneAsync(filter, replacement)`: Ele encontra o primeiro documento que corresponde ao `filter` e o **substitui completamente**.
6. `DeleteOneAsync(filter)`:Encontra o primeiro documento que corresponde ao `filter` e o **remove** da coleção. O método retorna um`DeleteResult` que contém informações sobre a operação, como a propriedade `DeletedCount`, que usamo
7. s para verificar se algo foi de fato excluído.