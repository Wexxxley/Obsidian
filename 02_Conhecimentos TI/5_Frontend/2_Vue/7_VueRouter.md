


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

![](../../../attachments/Pasted%20image%2020260831173342.png)![200](../../../attachments/Pasted%20image%2020260831172719.png)![400](../../../attachments/Pasted%20image%2020260831173422.png)
- **createWebHistory**: Função que habilita o modo de histórico HTML5. Ela permite que a aplicação utilize URLs limpas e padronizadas, sem a presença do caractere de fragmento #.
![400](../../../attachments/Pasted%20image%2020260831164002.png)![](../../../attachments/Pasted%20image%2020260831173515.png)
- **router-link**: Componente destinado à criação dos elos de navegação. 
- **router-view**: Componente que opera como um espaço reservado. Ele determina o local exato na hierarquia do layout onde o componente associado à URL atual será injetado e exibido.


  