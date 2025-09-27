
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

- **Arquitetura**: A Web opera na arquitetura cliente-servidor, onde os **navegadores** atuam como clientes e os **servidores Web** atuam como servidores.
- **Protocolo**: A interação entre eles é regida pelo **HTTP (HyperText Transfer Protocol)**, um protocolo do tipo requisição-resposta.
    - O cliente envia uma mensagem de **requisição HTTP** (com um método como `GET` para solicitar um recurso).
    - O servidor, se encontrar o recurso, envia de volta uma mensagem de resposta.
        
