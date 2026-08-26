
---
### 1. defineModel

Quando o usuário digita ou interage com o componente filho, o valor é atualizado localmente. O compilador do Vue intercepta essa mutação e injeta o novo dado diretamente na variável do componente pai.
    
- **A Regra de Aplicação:** O `defineModel` deve ser utilizado **estritamente para coleta de dados**. Sua aplicação é correta apenas quando o componente filho representa fisicamente um controle de formulário (como um campo de texto, uma caixa de seleção, um calendário ou um interruptor visual). O objetivo é garantir que pai e filho possuam o mesmo dado em memória em todo e qualquer instante.
![300](../../../attachments/Pasted%20image%2020260826084626.png)![500](../../../attachments/Pasted%20image%2020260826084520.png)Componente pai simples. Possui dois estados reativos. Chama o componente de Formulário e passa os valores pedidos para o componente via v-model.
![600](../../../attachments/Pasted%20image%2020260826084548.png)Componente que possui dois defineModel nomeados
### 2. defineEmits (Delegação de Eventos)

- **Definição do Conceito:** É um sistema de notificação unidirecional. O `defineEmits` atua como um mensageiro, permitindo que o componente filho informe ao componente pai que uma interação física específica foi realizada pelo usuário na interface.
    
- **Mecânica de Funcionamento:** O componente filho intercepta um evento do navegador (como um clique do mouse) e dispara um sinal nomeado (como `confirmar-acao`). Após emitir o sinal, o ciclo de vida do componente filho é encerrado para aquela ação. Ele não toma decisões sistêmicas nem altera variáveis. O componente pai monitora o surgimento desse sinal na árvore de renderização e, ao interceptá-lo, invoca uma função própria que contém os algoritmos lógicos e as regras de negócio do sistema.
    
- **A Regra de Aplicação:** O `defineEmits` deve ser utilizado **estritamente para acionar lógicas de processamento**. Sua aplicação é obrigatória quando a ação do usuário requer a execução de uma rotina, como validar senhas, enviar requisições HTTP para uma API externa (como salvar registros no banco de dados) ou recalcular valores matemáticos em matrizes de dados.
    

### Síntese de Decisão Arquitetural

- Se o componente filho precisa **fornecer um dado** para o pai (o que foi digitado), aplique o `defineModel`.
    
- Se o componente filho precisa **ordenar uma execução** para o pai (o comando de submissão), aplique o `defineEmits`.