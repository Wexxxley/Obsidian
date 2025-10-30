


---
### 1. Deployment Contínuo vs. Integração Contínua

- **Integração Contínua (CI):** Garante que o código dos desenvolvedores seja integrado _frequentemente_ (ex: diariamente) no _branch_ principal, passando por _build_ e _testes automatizados_. Mas esse código não precisa estar pronto para produção; pode ser uma funcionalidade incompleta ou com problemas de desempenho .
    
- **Deployment Contínuo (CD):** Com CD, todo _commit_ que passa com sucesso pelo processo de CI (build e todos os testes) é  implantado em produção, muitas vezes em questão de horas .
    
**O Fluxo de Trabalho com Deployment Contínuo:**
1. O desenvolvedor testa localmente e faz o _commit_.
2. O Servidor de CI executa o _build_ e os testes rápidos.    
3. Se passar, o servidor executa testes mais exaustivos (testes de integração, testes de interface, testes de desempenho).
4. Se **todos** os testes passarem, o sistema é **automaticamente implantado em produção**.

**Vantagens do Deployment Contínuo:**
- **Reduz o tempo de entrega:** Novas funcionalidades chegam aos usuários assim que ficam prontas, em vez de esperar meses por uma grande _release_. O resultado são _releases_ menores e mais frequentes
- **Feedback rápido e motivação:** Os desenvolvedores veem seu trabalho em produção rapidamente e recebem feedback de usuários reais.
- **Favorece experimentação:** Permite validar ideias rapidamente com usuários reais e, se necessário, cancelar ou alterar funcionalidades.

---
### **2. Entrega Contínua**

Deployment Contínuo não é recomendável para todos os sistemas, como aplicativos desktop ou mobile, onde o usuário teria que atualizar o app várias vezes ao dia. Para esses casos, existe uma variação, a entrega continua.

O fluxo é o mesmo do Deployment Contínuo, a diferença é que a implantação final em produção não é automática. Ela requer uma **autorização manual** (ex: um gerente de produto aperta o "botão" para liberar a _release_ para a loja de aplicativos).

Empresas de software não-Web (como Google Chrome, Eclipse, Facebook App) têm usado a Entrega Contínua para encurtar seus ciclos de _release_ entregando valor mais rápido.

---
### **3. Feature Flags** 

Se estamos usando Integração Contínua (commitando todo dia no _master_) e Deployment Contínuo (tudo no _master_ vai para produção), como fazemos para trabalhar em uma funcionalidade grande que levará semanas, sem quebrar a produção com código incompleto?
    
- **Solução:** Integre o código incompleto no _master_, mas "esconda-o" atrás de uma **Feature Flag**.
    
    ```java
     // O flag fica desabilitado em produção
     featureX = false;
     
     if (featureX) {
      // aqui vai o código novo e incompleto da funcionalidade X
     } else {
      // aqui fica o código antigo, que continua funcionando em produção
     }
    ```
    
- O desenvolvedor habilita o _flag_ (featureX = true) apenas em sua máquina local para testar a nova funcionalidade. Quando a funcionalidade X estiver pronta, o _flag_ é ativado em produção. 
- Em vez de variáveis fixas no código, _flags_ são geralmente gerenciados por bibliotecas ou arquivos de configuração, permitindo ligar ou desligar funcionalidades em produção sem precisar recompilar ou reimplantar o código.
    