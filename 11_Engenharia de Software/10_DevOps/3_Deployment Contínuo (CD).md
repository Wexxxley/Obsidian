


---

### Deployment Contínuo vs. Integração Contínua (CI)

Primeiro, é crucial entender a diferença:

- **Integração Contínua (CI):** Garante que o código dos desenvolvedores seja integrado _frequentemente_ (ex: diariamente) no _branch_ principal, passando por _build_ e _testes automatizados_. **Mas esse código não precisa estar pronto para produção**; pode ser uma funcionalidade incompleta ou com problemas de desempenho 1.
    
- **Deployment Contínuo (CD):** É o próximo passo. Com CD, todo _commit_ que passa com sucesso pelo processo de CI (build e todos os testes) é **automaticamente implantado em produção**, muitas vezes em questão de horas 2.
    

**O Fluxo de Trabalho com Deployment Contínuo:**

1. O desenvolvedor testa localmente e faz o _commit_3.
    
2. O Servidor de CI executa o _build_ e os testes rápidos (ex: testes de unidade)4.
    
3. Se passar, o servidor executa testes mais exaustivos (testes de integração, testes de interface, testes de desempenho) 5.
    
4. Se **todos** os testes passarem, o sistema é **automaticamente implantado em produção** 6.
    

**Vantagens do Deployment Contínuo:**

- **Reduz o tempo de entrega:** Novas funcionalidades chegam aos usuários assim que ficam prontas, em vez de esperar meses por uma grande _release_. O resultado são _releases_ menores e mais frequentes 7.
    
- **Implantação vira um "não-evento":** Remove o estresse e a pressão dos _deadlines_ de entrega 8.
    
- **Feedback rápido e motivação:** Os desenvolvedores veem seu trabalho em produção rapidamente e recebem feedback de usuários reais (em vez de esperar meses) 9.
    
- **Favorece experimentação:** Permite validar ideias rapidamente com usuários reais e, se necessário, cancelar ou alterar funcionalidades (como vimos nos Testes A/B e MVPs) 10.
    
- **Requer código pequeno:** Para funcionar, o CD exige que os desenvolvedores quebrem tarefas complexas em partes muito pequenas que possam ser implementadas e entregues rapidamente (como o Facebook, que implanta mudanças de, em média, 92 linhas de código) 11.
    

---

Entrega Contínua (Continuous Delivery)

Deployment Contínuo (automático) não é recomendável para todos os sistemas, como aplicativos desktop ou mobile, onde o usuário teria que atualizar o app várias vezes ao dia 12.

Para esses casos, existe uma variação mais "fraca":

- **Entrega Contínua (Continuous Delivery):**
    
    - O fluxo é o mesmo do Deployment Contínuo: todo _commit_ passa por _build_ e testes automatizados, ficando **tecnicamente pronto para ir à produção** 13.
        
    - **A diferença chave:** A implantação final em produção **não é automática**. Ela requer uma **autorização manual** (ex: um gerente de produto aperta o "botão" para liberar a _release_ para a loja de aplicativos) 14141414.
        
- **Resumo da Diferença:**
    
    - **Delivery (Entrega):** Deixar a nova versão _pronta_ para implantação.
        
    - **Deployment (Implantação):** Liberar a nova versão para os _usuários_.
        
    - Em Deployment Contínuo, ambos são automáticos. Em Entrega Contínua, a _Delivery_ é automática, mas o _Deployment_ é manual.
        

Empresas de software não-Web (como Google Chrome, Eclipse, Facebook App) têm usado a Entrega Contínua para encurtar seus ciclos de _release_ de anuais para semestrais, trimestrais ou até semanais, entregando valor mais rápido 15.

---

**Feature Flags (ou Feature Toggles)**

- **O Problema:** Se estamos usando Integração Contínua (commitando todo dia no _master_) e Deployment Contínuo (tudo no _master_ vai para produção), como fazemos para trabalhar em uma funcionalidade grande (X) que levará semanas, sem quebrar a produção com código incompleto? 16
    
- **A Solução:** Integre o código incompleto no _master_, mas "esconda-o" atrás de uma **Feature Flag** (uma variável booleana)17.
    
- **Exemplo:**
    
    Java
    
    ```
     // O flag fica desabilitado em produção
     featureX = false;
     ...
     if (featureX) {
      // aqui vai o código novo e incompleto da funcionalidade X
     } else {
      // aqui fica o código antigo, que continua funcionando em produção
     }
    ```
    
- O desenvolvedor habilita o _flag_ (`featureX = true`) **apenas em sua máquina local** para testar a nova funcionalidade. Quando a funcionalidade X estiver pronta, o _flag_ é ativado em produção. Eventualmente, o _flag_ e o código antigo são removidos 18.
    
- **Outros Usos de Feature Flags:**
    
    - **Release Canário:** Liberar a nova funcionalidade (com o _flag_ ligado) apenas para um grupo pequeno de usuários (ex: 5%) para monitorar problemas antes de liberar para todos 19.
        
    - **Testes A/B:** Usar _flags_ para direcionar diferentes usuários para diferentes versões de uma funcionalidade e comparar os resultados (como vimos no Cap. 3) 20.
        
- **Gerenciamento:** Em vez de variáveis fixas no código, _flags_ são geralmente gerenciados por bibliotecas ou arquivos de configuração, permitindo ligar ou desligar funcionalidades em produção sem precisar recompilar ou reimplantar o código 21.
    

Com isso, fechamos o Capítulo 10 e a visão geral do livro sobre DevOps.

O que você gostaria de fazer agora? Podemos revisar algum capítulo ou conceito específico?