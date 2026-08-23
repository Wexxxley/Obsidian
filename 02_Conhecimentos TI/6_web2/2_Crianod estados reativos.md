
Sistema de reatividade do Vue. O DOM é atualizado de forma autônoma sempre que as variáveis em memória sofrem alterações.
### **1. COM REF**
![500](../../attachments/Pasted%20image%2020260823142734.png)![200](../../attachments/Pasted%20image%2020260823142817.png)
- **.value:** usado para acessar o valor das variáveis reativas.
- **Chaves duplas**: sintaxe Mustache. usado para extrair texto e escrever funções js no HTML.
- A diretiva `@click` atua como um listener. A interação do usuário aciona a função incrementar.s

Você não é obrigado a definir o tipo explicitamente utilizando a notação de diamantes na ref. Quando você fornece um valor inicial, o compilador do TS executa a inferência de tipo. 
- `const nome = ref('Sistema');` Infere o tipo como `Ref<string>`.
- `const ativo = ref(true);` Infere o tipo como `Ref<boolean>`.
    
A declaração explícita torna-se  necessária quando o tipo não pode ser inferido facilmente ou quando a variável precisa armazenar estruturas de dados complexas.
- **Arrays:** `const lista = ref<string[]>(['Item 1', 'Item 2']);`
- **Múltiplos Tipos:** `const id = ref<string | number>(123);` permite que a variável aceite tanto números quanto cadeias de caracteres.      
- **Tipagem com Null:** `const token = ref<string | null>(null);` Utilizar `null` é a abordagem recomendada quando você deseja declarar intencionalmente que o estado está  vazio e aguardando processamento.

---
### **2. COM REACTIVE**

A principal diferença em relação ao ref é que a reatividade gerada pelo reactive é profunda por padrão. Isso significa que, se você instanciar um objeto com múltiplos níveis de aninhamento (como objetos dentro de objetos), todas as propriedades em todos os níveis da hierarquia serão monitoradas de forma autônoma.
-  Permite que o acesso ocorra através da notação de ponto padrão.

**Limitações**
1. **Bloqueio de Tipos Primitivos:** rejeita a injeção de tipos primitivos isolados.
2. **Perda de Reatividade na Desestruturação:** Se você tentar extrair uma propriedade isolada do objeto reativo utilizando a sintaxe de desestruturação padrão do JavaScript, a variável resultante será extraída como um dado estático comum.
    


```
<script setup lang="ts">
import { reactive } from 'vue';

// Declaração de um estado complexo (inferência de tipo automática baseada no objeto)
const usuario = reactive({
  nome: 'Sistema',
  permissoes: ['leitura', 'escrita'],
  configuracoes: {
    temaEscuro: true
  }
});

// Mutação direta da propriedade sem a necessidade do sufixo .value
function alternarTema() {
  usuario.configuracoes.temaEscuro = !usuario.configuracoes.temaEscuro;
}
</script>

<template>
  <main>
    <h1>Usuário: {{ usuario.nome }}</h1>
    <!-- O Vue processa objetos aninhados normalmente na interpolação -->
    <p>Tema escuro ativado: {{ usuario.configuracoes.temaEscuro }}</p>
    <button @click="alternarTema">Modificar Configuração</button>
  </main>
</template>
```