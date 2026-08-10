
#Concluded 

---

Vamos implementar a funcionalidade de **remover um item** da lista. Isso exige transformar a lista `stories` em um estado (para que possa ser modificada) e aprender a passar argumentos para handlers de eventos.

![](../../../../attachments/Pasted%20image%2020251124191100.png)
![](../../../../attachments/Pasted%20image%2020251124191041.png)

**Análise Técnica:** A sintaxe `() => onRemoveItem(item)` cria uma nova função anônima a cada renderização do `Item`. Quando o usuário clica, essa função anônima é executada e, dentro dela, a função `onRemoveItem` é chamada com o argumento `item` que está disponível no escopo (closure).