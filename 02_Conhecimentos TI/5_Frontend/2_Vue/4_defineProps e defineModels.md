

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

Os dados são sincronizados entre o pai e o filho em ambas as direções. O componente filho tem permissão  para alterar o valor do dado. Quando essa modificação ocorre localmente no filho, o motor do Vue intercepta a alteração e atualiza a variável no componente pai.
    
- **Utilize defineModel:**  quando o componente filho for projetado para coletar interações e alterar o estado do sistema, como em campos de entrada de formulários.

![300](../../../attachments/Pasted%20image%2020260826084626.png)![500](../../../attachments/Pasted%20image%2020260826084520.png)Componente pai simples. Possui dois estados reativos. Chama o componente de Formulário e passa os valores pedidos para o componente via v-model.
![600](../../../attachments/Pasted%20image%2020260826084548.png)Componente que possui dois defineModel
