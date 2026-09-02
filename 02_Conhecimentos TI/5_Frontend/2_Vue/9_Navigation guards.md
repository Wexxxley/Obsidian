

---

Os Navigation Guards são funções de interceptação que permitem pausar, redirecionar ou cancelar o processo de transição entre as rotas do sistema.
- A aplicação primária ocorre no controle de acesso e autorização. redireciona se necessário para a tela de login.
- Outra exemplo é o bloqueio da saída de uma página caso o sistema detecte que o usuário possui um formulário preenchido com alterações não salvas.
![](../../../attachments/Pasted%20image%2020260902102559.png)
-  **beforeRouteLeave**: Acionado dentro do componente atual, tendo como função primária bloquear a navegação caso existam processos inconclusos.
- **beforeEach**: Opera em escopo global. É nesta etapa que ocorrem as inspeções de autenticação e a verificação de credenciais.
- **Avaliação**: O sistema avalia se o componente será reutilizado. Por exemplo, a mudança da URL `/livro/1` para `/livro/2`.
- **beforeRouteUpdate**: Se o componente permanecer na tela. Permite que os estados reativos sejam atualizados com os novos dados da URL sem a necessidade de destruir o componente.
- **beforeEnter**: 
- **beforeRouteEnter**: Por ser executado antes da instância do componente existir fisicamente na memória, este guardião não possui acesso às variáveis ou métodos locais.
- **beforeResolve**: Sua execução garante que todos os guardiões anteriores foram resolvidos de forma bem-sucedida.
- **afterEach**: é utilizado para efeitos colaterais pós-renderização.

Os guardiões podem ser injetados no ciclo de vida do roteamento em três níveis:
- **Guardiões Globais:** Declarados na instância do roteador. Eles são acionados a cada solicitação de mudança de rota em toda a aplicação.
	-  beforeEach, beforeResolve e afterEach
- **Guardiões por Rota:** Definidos dentro do objeto de configuração no arquivo de rotas. A sua execução ocorre quando o sistema tenta processar aquela rota específica.
	- beforeEnter
- **Guardiões por Componente:** Declarados no arquivo do componente. Monitoram transições que afetam o estado do componente.
	- beforeRouteEnter, beforeRouteUpdate e beforeRouteLeave.

Independentemente do escopo, toda função de um guardião recebe dois objetos injetados:
- **to:** Contém a estrutura de dados completa da rota de destino.
- **from:** Contém a estrutura de dados da rota de origem, representando a URL atual.

![300](../../../attachments/Pasted%20image%2020260902101958.png)![600](../../../attachments/Pasted%20image%2020260902104703.png)
- **BeforeEach**: Guarda global. Toda vez que uma navegação for realizada ele é executado.
- **BefoceEnter:** Guarda de rota. So é executado naquela rota específica.

![](../../../attachments/Pasted%20image%2020260902105616.png)
- **onBeforeRouteLeave:** Guarda de componente.
- **onMounted:** Executa a injeção do evento assim que o componente de formulário é construído.
- **beforeunload**: um evento da interface global Window do navegador. Ele é disparado quandoem que a janela está prestes a ser descarregada da memória.
- **onBeforeUnmount:** Remove a escuta do evento instantes antes de o componente ser destruído. A omissão dessa etapa gera um vazamento de memória, fazendo com que o navegador continue bloqueando a aba.