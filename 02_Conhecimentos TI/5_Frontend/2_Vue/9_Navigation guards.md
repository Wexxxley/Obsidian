

---


Os Navigation Guards são funções de interceptação que operam como pontos de checagem lógicos que permitem pausar, redirecionar ou cancelar permanentemente o processo de transição entre as rotas do sistema.

- A aplicação primária ocorre no controle de acesso e autorização. O guardião intercepta a requisição para uma rota privada, inspeciona a memória do sistema em busca de um token de sessão válido. Se não for encontrada, ele redireciona para a tela de login.
- Outra exemplo é o bloqueio da saída de uma página caso o sistema detecte que o usuário possui um formulário preenchido com alterações não salvas.

Os guardiões podem ser injetados no ciclo de vida do roteamento em três níveis:
- **Guardiões Globais:** Declarados na instância do roteador (`router.beforeEach`). Eles são acionados a cada solicitação de mudança de rota em toda a aplicação.
- **Guardiões por Rota:** Definidos dentro do objeto de configuração no arquivo de rotas (`beforeEnter`). A sua execução ocorre quando o sistema tenta processar aquela rota específica.
- **Guardiões por Componente:** Declarados no arquivo do componente. (`onBeforeRouteLeave` ou `onBeforeRouteUpdate`). Monitoram transições que afetam o estado do componente.


Independentemente do escopo, toda função de um guardião recebe dois objetos injetados:
- **to:** Contém a estrutura de dados completa da rota de destino, informando exatamente qual URL, nome e parâmetros o sistema está tentando acessar.
- **from:** Contém a estrutura de dados da rota de origem, representando a URL atual onde o usuário se encontra antes do clique.
    