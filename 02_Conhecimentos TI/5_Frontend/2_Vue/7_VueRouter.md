


---

**Multi-Page Application (MPA):** Na arquitetura tradicional, cada interação que exigia uma nova visualização (como clicar em um link) forçava o navegador a enviar uma nova requisição ao servidor. 
- O servidor processava a requisição, construía um documento HTML e o enviava de volta.
- O navegador destruía a página atual e renderizava o novo documento HTML, o que gerava o efeito visual de "tela branca" ou "piscar" durante a transição.

**A Abordagem SPA:**: A aplicação entrega apenas um arquivo HTML base na primeira requisição, juntamente com os arquivos JavaScript e CSS necessários.
- Quando o usuário navega para uma nova seção, o JavaScript intercepta a ação. O navegador não requisita uma nova página HTML.
- Em vez de solicitar páginas visuais completas, a aplicação solicita ao servidor apenas os dados brutos necessários.
-  JavaScript recebe esses dados e os utiliza para modificar apenas a área específica da página que precisa ser alterada. O restante da interface permanece intacto.

---
### 1. Vue router

O Vue Router é a biblioteca oficial de roteamento. Ela viabilizaa a construção de Aplicações de Single Page Applications. 

```
npm install vue-router@4
```

A implementação do Vue Router requer a criação de uma instância de roteador e a definição das rotas. Uma rota é um objeto JS que estabelece a correlação entre uma string de URL e um componente Vue específico.
  ![200](../../../attachments/Pasted%20image%2020260831163559.png)![400](../../../attachments/Pasted%20image%2020260831163632.png)
- **createWebHistory**: Função que habilita o modo de histórico HTML5. Ela permite que a aplicação utilize URLs limpas e padronizadas, sem a presença do caractere de fragmento #.
![400](../../../attachments/Pasted%20image%2020260831164002.png)![](../../../attachments/Pasted%20image%2020260831163720.png)
- **router-link**: Componente destinado à criação dos elos de navegação. 
- **router-view**: Componente funcional que opera como um contêiner ou espaço reservado. Ele determina o local exato na hierarquia do layout onde o componente associado à URL atual será injetado e exibido.
    





### Aplicação Prática no Template (exemplo em `src/App.vue`)

Snippet de código

```
<template>
  <header>
    <nav>
      <!-- Navegação utilizando as rotas definidas -->
      <router-link to="/">Página Inicial</router-link>
      <router-link to="/about">Sobre Nós</router-link>
    </nav>
  </header>

  <main>
    <!-- Local de renderização dinâmica -->
    <router-view></router-view>
  </main>
</template>
```