
#Concluded 

---
Para ilustrar os conceitos de sistemas distribuídos, vamos usar a **World Wide Web (WWW)** como um estudo de caso detalhado. A Web é um sistema em evolução para publicar e acessar recursos e serviços pela Internet.

A Web é um **sistema aberto** que pode ser ampliado e reimplementado sem perturbar a funcionalidade existente. Sua operação é baseada em três componentes  padrão:
#### **1. HTML**
- É a linguagem usada para especificar o conteúdo (textos, imagens) e o leiaute de uma página Web3. Uma característica fundamental é que a HTML permite a criação de **links (ou hyperlinks)** para outros documentos e recursos na Web. É essa estrutura de links que forma a "teia".
#### **2. URLs (Uniform Resource Locators)**
- URLs são usados para identificar de forma única recursos armazenados na Web. Um URL HTTP completo (como`http://www.cdk5.net/index.html`) tem duas tarefas principais:
    1. Identificar qual **servidor Web** mantém o recurso (ex: `www.cdk5.net`).
    2. Identificar **qual recurso** está sendo solicitado nesse servidor (ex: `index.html`).

- ==**Estrutura**: http://nomedoservidor[:porta][/nomedeCaminho][?consulta][#fragmento].==

#### **3. Arquitetura Cliente-Servidor e HTTP**

- **Arquitetura**: A Web opera em uma arquitetura cliente-servidor, onde os **navegadores (browsers)** atuam como clientes e os **servidores Web** atuam como servidores99.
    
- **Protocolo**: A interação entre eles é regida pelo **HTTP (HyperText Transfer Protocol)**, um protocolo do tipo requisição-resposta101010.
    
    - O cliente envia uma mensagem de **requisição HTTP** (com um método como `GET` para solicitar um recurso).
        
    - O servidor, se encontrar o recurso, envia de volta uma
        
        **mensagem de resposta HTTP** contendo os dados do recurso e um código de status (como o famoso `404 Not Found` se o recurso não existir)11.
        

##### **Recursos Avançados da Web**

- **Páginas Dinâmicas**: Nem todo conteúdo da Web é estático (armazenado em arquivos). Muitos recursos são gerados dinamicamente por programas no servidor (como scripts **CGI** ou **servlets**) em resposta a uma entrada do usuário, como o preenchimento de um formulário. Para o navegador, o conteúdo gerado dinamicamente é transparente, pois ele o recebe como um texto HTML normal12.
    
- **Código Baixado**: Para melhorar a interatividade, a Web permite que código seja baixado do servidor e executado no cliente. Exemplos incluem
    
    **Javascript**, que pode validar formulários instantaneamente, e **applets Java**, que são aplicações completas executadas dentro do navegador13.
    
- **Serviços Web**: A Web evoluiu para permitir que programas, e não apenas usuários com navegadores, acessem seus recursos. Usando
    
    **XML (Extensible Markup Language)** para representar dados estruturados, os **serviços Web** permitem que aplicações interajam com servidores de forma programática, trocando dados estruturados em vez de apenas páginas HTML para exibição14.
    

Com isso, concluímos a explanação do Capítulo 1, que define o que são sistemas distribuídos, explora suas tendências e desafios, e usa a Web como um exemplo prático de um sistema distribuído de grande escala.