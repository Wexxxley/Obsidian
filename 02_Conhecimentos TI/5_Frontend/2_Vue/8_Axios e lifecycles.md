



---
### 1. Axios

O Axios é uma biblioteca JavaScript que estabelece a comunicação entre o aplicativo front-end e um servidor back-end ou uma API. Permite o envio de requisições para buscar, inserir, atualizar ou excluir dados.
- O funcionamento do Axios é baseado em **Promises**. Uma promise é um objeto que representa a eventual conclusão ou falha de uma operação assíncrona.

```
npm install axios
```

Geralmente, as chamadas para a API são engatilhadas utilizando os **Lifecycle Hooks** do Vue. O gancho mais utilizado para isso é o `onMounted`. Ele instrui o Vue a executar uma determinada função imediatamente após o componente ser montado e renderizado no DOM, garantindo que os dados sejam buscados assim que o usuário acessar a tela correspondente.
![](../../../attachments/Pasted%20image%2020260831180244.png)

---
### 2. Hooks lifecycles

Cada instância de um componente passa por uma série de etapas de inicialização quando é criada. O Vue executa funções específicas chamadas de Lifecycle Hooks , que permitem ao desenvolvedor injetar seu próprio código em estágios específicos.
![](../../../attachments/Pasted%20image%2020260831181040.png)
- **setup**: Quando você utiliza a estrutura `<script setup>`, o código é executado antes mesmo de o componente ser criado. É o primeiro código a ser rodado, responsável por inicializar as variáveis reativas e declarar funções. Não há um "gancho" explícito para chamar aqui.
- **beforeMount:** Este gancho é acionado antes do início da montagem do componente. Neste momento, o Vue já terminou de compilar o HTML e processar as lógicas reativas, mas o componente ainda não foi inserido no DOM. Não é muito usado.
- **onMounted:** Este é o gancho acionado após o componente ter sido montado e inserido no DOM. Este é o local ideal para realizar operações que exigem acesso direto aos elementos HTML da página ou para iniciar a busca de dados assíncronos.![](../../../attachments/Pasted%20image%2020260831181643.png)
- **onBeforeUpdate:** Este gancho é acionado quando ocorre uma alteração em algum dado reativo, mas antes que o Vue aplique essa alteração. Ele permite que o desenvolvedor leia o estado atual do elemento HTML antes que ele seja re-renderizado com os novos dados.
- **onUpdated:** Este gancho é acionado após uma alteração de dado reativo ter causado uma atualização na árvore do DOM. 
- **onBeforeUnmount:** Acionado antes de a instância do componente ser desmontada e removida da interface.
- **onUnmounted:** Acionado após o componente ter sido completamente desmontado. Este é o local exigido pela arquitetura do Vue para realizar limpezas de memória.