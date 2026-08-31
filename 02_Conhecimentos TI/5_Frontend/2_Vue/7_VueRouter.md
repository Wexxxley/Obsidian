


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

  

### 1. Definição das Rotas (geralmente em `src/router/index.js`)

Este arquivo centraliza a lógica de roteamento. É necessário importar as funções fundamentais da biblioteca e os componentes que atuarão como páginas.

  

JavaScript

```
import { createRouter, createWebHistory } from 'vue-router'
import HomeView from '../views/HomeView.vue'
import AboutView from '../views/AboutView.vue'

// Definição do vetor de rotas
const routes = [
  {
    path: '/',
    name: 'home',
    component: HomeView
  },
  {
    path: '/about',
    name: 'about',
    component: AboutView
  }
]

// Instanciação do roteador
const router = createRouter({
  history: createWebHistory(),
  routes
})

export default router
```

- **`createRouter`**: Função responsável por instanciar o roteador com os parâmetros fornecidos.
    
      
    
- **`createWebHistory`**: Função que habilita o modo de histórico HTML5. Ela permite que a aplicação utilize URLs limpas e padronizadas, sem a presença do caractere de fragmento (`#`).
    
      
    

### 2. Injeção na Instância Principal (`src/main.js`)

Para que as regras definidas entrem em vigor, o roteador exportado deve ser injetado na instância principal da aplicação Vue.

  

JavaScript

```
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'

const app = createApp(App)

// Registro do roteador na aplicação
app.use(router)
app.mount('#app')
```

## Componentes de Interface

Com o roteador devidamente configurado e registrado, a aplicação disponibiliza dois componentes globais que devem ser utilizados nos arquivos de marcação (templates) para efetivar a navegação e a renderização.

  

- **`<router-link>`**: Componente destinado à criação de elos de navegação. Ele exige a propriedade `to`, que estipula o caminho de destino. Embora seja renderizado no navegador como uma tag de âncora padrão (`<a>`), o `<router-link>` intercepta o evento de clique, prevenindo o recarregamento total da página e instruindo o Vue Router a processar a transição interna.
    
      
    
- **`<router-view>`**: Componente funcional que opera como um contêiner ou espaço reservado. Ele determina o local exato na hierarquia do layout onde o componente associado à URL atual será injetado e exibido.
    

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