

---

![](../../attachments/Pasted%20image%2020260321103319.png)

---
### **1. Lazy Colum** 

A LazyColumn é um componente de lista vertical que utiliza um algoritmo de virtualização para renderizar apenas os itens visíveis na tela. Diferente de uma coluna comum, ela não carrega todos os dados na memória de uma vez. À medida que o usuário realiza o scroll, os itens que saem da área de visão são descartados e os novos são compostos em tempo real. Isso otimiza o uso de CPU e RAM, permitindo a exibição de milhares de registros sem comprometer a fluidez da interface.

**Exemplo**
![](../../attachments/Pasted%20image%2020260323070253.png)
![](../../attachments/Pasted%20image%2020260323070310.png)
- Foi usado o **mutableStateListOf** para caso a lista for alterada o Compose dispara uma recomposição na interface.
- O **remember** garante que a lista não seja reinicializada toda vez que a função for executada novamente.

![550](../../attachments/Pasted%20image%2020260323073234.png)
- **TopAppBarDefaults.pinnedScrollBehavior()**: Esta função cria um comportamento onde a topbar fica fixa, mas ela sabe quando o conteúdo está passando por baixo dela.
- No **Scaffold**, você usa **topBarBehavior.nestedScrollConnection.** Quando o usuário arrasta a lista, o evento de scroll é enviado para o topBarBehavior. 
- **scrolledContainerColor**: Quando o sensor de scroll detecta que a lista não está no t
- **items(count = countryList.size)**: É um iterador. Para cada índice, ele cria o card.