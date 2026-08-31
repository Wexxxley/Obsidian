


---

O Axios é uma biblioteca JavaScript que estabelece a comunicação entre o aplicativo front-end e um servidor back-end ou uma API. Permite o envio de requisições para buscar, inserir, atualizar ou excluir dados.
- O funcionamento do Axios é baseado em **Promises**. Uma promise é um objeto que representa a eventual conclusão ou falha de uma operação assíncrona.

```
npm install axios
```

Geralmente, as chamadas para a API são engatilhadas utilizando os **Lifecycle Hooks** do Vue. O gancho mais utilizado para isso é o `onMounted`. Ele instrui o Vue a executar uma determinada função imediatamente após o componente ser montado e renderizado no DOM, garantindo que os dados sejam buscados assim que o usuário acessar a tela correspondente.

  

```
<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

// Variáveis reativas para gerenciar o estado da interface
const postagens = ref([]);
const carregando = ref(true);
const erro = ref(null);

// Função assíncrona responsável por fazer a requisição HTTP
const buscarDadosDaApi = async () => {
  try {
    // O Axios faz uma requisição do tipo GET para buscar os dados
    const resposta = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=5');
    
    // Os dados retornados pelo servidor ficam armazenados na propriedade "data"
    postagens.value = resposta.data;
  } catch (falha) {
    // Caso o servidor retorne um erro ou falte internet, capturamos a falha aqui
    erro.value = 'Ocorreu um erro de comunicação com o servidor ao buscar as postagens.';
    console.error(falha);
  } finally {
    // O bloco "finally" é executado independentemente de sucesso ou falha na requisição
    carregando.value = false;
  }
};

// O gancho onMounted executa a função assim que o componente é inserido na tela
onMounted(() => {
  buscarDadosDaApi();
});
</script>

<template>
  <div class="page-container home-page">
    <h1>🏠 Página Inicial</h1>
    <p>Bem-vindo ao nosso aplicativo com Vue Router e integração com Axios!</p>
    <p>Abaixo, os dados buscados do servidor:</p>

    <!-- Estrutura condicional para exibir o estado atual da requisição -->
    <div class="dados-api">
      <!-- Exibe uma mensagem enquanto a Promise não for resolvida -->
      <p v-if="carregando"><strong>Buscando informações no servidor...</strong></p>

      <!-- Exibe uma mensagem de erro caso a requisição falhe -->
      <p v-else-if="erro" class="mensagem-erro">{{ erro }}</p>

      <!-- Renderiza a lista de dados caso a requisição seja bem-sucedida -->
      <ul v-else>
        <li v-for="postagem in postagens" :key="postagem.id">
          {{ postagem.title }}
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.home-page {
  background-color: #e8f5e9;
  border-left: 6px solid #4caf50;
}

.dados-api {
  margin-top: 30px;
  padding: 15px;
  background-color: #ffffff;
  border: 1px solid #c8e6c9;
  border-radius: 4px;
}

.mensagem-erro {
  color: #d32f2f;
  font-weight: 500;
}
</style>
```

Nesta estrutura, as variáveis `postagens`, `carregando` e `erro` reagem dinamicamente. Enquanto a requisição HTTP está em trânsito (aguardando a resposta do servidor), a interface exibe o texto de carregamento. Assim que o Axios recebe e processa a resposta, o Vue detecta a alteração nos dados e atualiza a tela automaticamente com a lista gerada pela diretiva `v-for`.