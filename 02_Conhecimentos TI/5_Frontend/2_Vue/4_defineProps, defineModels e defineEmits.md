
#Concluded 

---
### 1. defineProps
Mecanismo oficial para a transferência unidirecional de dados do componente pai para o componente filho. Dados READ-ONLY.

Para atualizar o dado, o filho deve emitir um sinal defineEmits solicitando que o pai faça a alteração na fonte original.

- **Utilize defineProps:** Quando o componente filho for apenas um consumidor visual da informação, como um cartão de perfil exibindo o nome de um usuário.
![500](../../../attachments/Pasted%20image%2020260824111352.png)![](../../../attachments/Pasted%20image%2020260824111336.png)
**1. Passagem de dado Estático:** você declara `titulo="Servidor Central"`.
**2. Passagem Dinâmica:** é preciso usar v-bind.

---
### 2. defineModel

Os dados são sincronizados entre o pai e o filho em ambas as direções. O componente filho tem permissão para alterar o valor do dado. Quando essa modificação ocorre localmente no filho, o motor do Vue intercepta a alteração e atualiza a variável no componente pai.
    
- **Utilize defineModel:**  quando o componente filho for projetado para coletar interações e alterar o estado do sistema, como em campos de entrada de formulários.

![300](../../../attachments/Pasted%20image%2020260826084626.png)![500](../../../attachments/Pasted%20image%2020260826084520.png)Componente pai simples. Possui dois estados reativos. Chama o componente de Formulário e passa os valores pedidos para o componente via v-model.
![600](../../../attachments/Pasted%20image%2020260826084548.png)Componente que possui dois defineModel

>[!tip]
**Ao usar defineProps:** o componente pai injeta o dado utilizando o `v-bind` 
**Ao usar defineModel:** o componente pai injeta o dado utilizando o `v-model`. Permitindo o fluxo de dados bidirecional.

---
### 3. defineEmits 

Permite que o componente filho informe ao componente pai que uma interação física específica foi realizada pelo usuário na interface.
- O componente filho intercepta um evento do navegador e dispara um sinal nomeado. O componente pai monitora o surgimento desse sinal e, ao interceptá-lo, invoca uma função própria que contém os algoritmos lógicos e as regras de negócio do sistema.
- **Quando usar:** estritamente para acionar lógicas de processamento.

>[!TIP]
>- Se o componente filho so precisa mostrar os dados do pai: **defineProps**.
>- Se o componente filho precisa fornecer um dado para o pai: **defineModel**.
>- Se o componente filho precisa ordenar uma execução para o pai: **defineEmits**.

![200](../../../attachments/Pasted%20image%2020260826093518.png)![450](../../../attachments/Pasted%20image%2020260826093444.png)O componente pai possui o estado reativo Catálogo e funções para adicionar e remover itens. Ao chamar o componente filho ele passa o PRODUTO como propriedade (readonly). E passa as funções que respondem aos eventos internos.
![550](../../../attachments/Pasted%20image%2020260826093406.png)O componente filho define a propriedade produto(readonly) e os eventos.