

---
### 1. Props
Props são atributos personalizados registrados na estrutura de um componente filho. Elas representam o mecanismo oficial para a transferência unidirecional de dados do componente pai para o componente filho.
![500](../../../attachments/Pasted%20image%2020260824111352.png)![](../../../attachments/Pasted%20image%2020260824111336.png)
**1. Passagem de dado Estático:** você declara `titulo="Servidor Central"`.
**2. Passagem Dinâmica:** é preciso usar v-bind.

---
### 2. Slots

Enquanto as Props transmitem dados processados e variáveis lógicas, os Slots transmitem estruturas de interface (elementos HTML ou outros componentes). 

**Componente Filho (`BotaoAcao.vue`):**

O componente filho define sua estrutura CSS e de comportamento, mas deixa uma área aberta (o slot) para que o texto ou ícone do botão seja definido externamente.

  

Snippet de código

```
<script setup lang="ts">
// Lógica interna do botão omitida
</script>

<template>
  <button class="estilo-padrao">
    <!-- O conteúdo injetado pelo pai será renderizado no lugar desta tag -->
    <slot></slot>
  </button>
</template>

<style scoped>
.estilo-padrao {
  padding: 10px 20px;
  background-color: #4CAF50;
  color: white;
}
</style>
```

**Componente Pai (`App.vue`):**

O pai instancia o componente filho e escreve o conteúdo HTML desejado estritamente entre as tags de abertura e fechamento do componente. O Vue compilará esse conteúdo e o transportará para o local exato do `<slot>`.

Snippet de código

```
<script setup lang="ts">
import BotaoAcao from './components/BotaoAcao.vue';
</script>

<template>
  <main>
    <!-- Instância 1: Injetando apenas um nó de texto -->
    <BotaoAcao>
      Confirmar Operação
    </BotaoAcao>

    <!-- Instância 2: Injetando marcação HTML (negrito) -->
    <BotaoAcao>
      <strong>Cancelar</strong> Operação
    </BotaoAcao>
  </main>
</template>
```