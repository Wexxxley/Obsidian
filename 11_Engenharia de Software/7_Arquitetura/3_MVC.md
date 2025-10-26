
#Concluded 

---

Surgiu na década de 80 com a proposta de  implementar interfaces gráficas (GUIs). O MVC não foi pensado para aplicações distribuídas; mas para aplicações desktop monolíticas como Microsoft Word, Calculadora, etc.
### **Componentes Principais** 
O MVC divide as classes de um sistema em três grupos principais com responsabilidades distintas:

1. **Visão (View):**    
    - Classes responsáveis pela **apresentação da interface gráfica** para o usuário.
        
2. **Controladoras (Controller):**
    - Classes que **tratam e interpretam eventos**. Ao receber um evento , a controladora pode solicitar uma alteração no estado do Modelo ou atualizar a Visão.
        
3. **Modelo (Model):**
    - Classes que **armazenam os dados** da aplicação e implementam a **lógica de negócio** (regras do domínio) .
    - **Importante:** Classes de Modelo **não têm conhecimento ou dependência** das classes de Visão ou Controladoras. Elas são independentes da interface.
    - Contêm os dados e os métodos que manipulam esses dados.

---
### **Interação e Dependências**

- A Interface Gráfica é formada pela combinação da Visão e dos controladores . Muitas vezes, na prática, a separação entre Visão e Controladora não é tão rígida .
    
- A **Interface Gráfica pode depender do Modelo** para exibir seus dados. Mas o **modelo NÃO depende da Interface Gráfica**.
    
- Geralmente, a Interface Gráfica atua como **observadora** do Modelo (usando o padrão Observer). Quando o estado do Modelo muda, ele notifica a Interface Gráfica para que ela se atualize .
    

---
### **Vantagens do MVC**

- **Separação de Responsabilidades e Especialização:** Permite que desenvolvedores se especializem (ex: front-end focado na Interface Gráfica, back-end focado no Modelo) .
    
- **Múltiplas Visões:** Permite que os mesmos dados do Modelo sejam apresentados de diferentes formas por diferentes Visões (ex: um relógio com a mesma hora mostrada em formato analógico e digital) .
    
- **Testabilidade:** Facilita os testes, especialmente do Modelo, pois ele pode ser testado independentemente da interface gráfica (que é geralmente mais difícil de testar automaticamente) .
    

    

**Pergunta Frequente: Qual a diferença entre MVC e Três Camadas?** A resposta envolve a evolução histórica:

1. **MVC Clássico (anos 70/80):** Focado em aplicações desktop com interfaces gráficas (como Smalltalk, ou pacotes Office) . Separa Modelo (dados/lógica) da Interface (Visão/Controlador) dentro da _mesma aplicação_.
    
2. **Três Camadas (anos 90):** Surge com redes e bancos de dados distribuídos. Separa fisicamente a **Apresentação** (cliente), a **Lógica de Negócio** (servidor de aplicação) e o **Banco de Dados** (servidor de BD) . Uma aplicação desktop seguindo MVC poderia ser a camada de apresentação de um sistema de três camadas .
    
3. **MVC para Web (anos 2000):** Com a popularização da Web, frameworks como Spring, Ruby on Rails, Django adotaram a terminologia MVC, mas adaptada . Neles:
    
    - **Visão:** Páginas HTML (geradas dinamicamente).
        
    - **Controlador:** Processa requisições HTTP e decide qual Visão gerar.
        
    - **Modelo:** Interage com o banco de dados (camada de persistência).
        
    - Essa estrutura **lembra muito a arquitetura em três camadas**, mas usa a nomenclatura MVC .
        

**Exemplo: Single Page Applications (SPAs)**

- São aplicações Web modernas (como o GMail) que carregam a maior parte do código (HTML, CSS, JS) para o navegador de uma vez .
    
- A interação do usuário ocorre principalmente no navegador, sem recarregar a página inteira a cada ação, proporcionando uma experiência mais fluida, similar a um desktop .
    
- A comunicação com o servidor ainda existe (ex: para buscar novos e-mails), mas é feita de forma assíncrona .
    
- Frameworks JavaScript para SPAs (como Vue.js, React, Angular) frequentemente seguem uma arquitetura parecida com MVC no lado do cliente (navegador) :
    
    - **Visão/Controle:** Implementados em HTML e manipulados pelo framework JS.
        
    - **Modelo:** Gerenciado pelo framework JS (ex: o objeto `data` no exemplo Vue.js).
        

Terminamos a seção sobre Arquitetura MVC. Digite "next" para passarmos para Microsserviços.