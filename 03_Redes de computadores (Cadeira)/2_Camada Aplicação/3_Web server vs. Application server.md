
#Concluded 

---
### **1. Servidor Web**

Um servidor Web hospeda o código e os dados de um site. Seu navegador e servidor Web se comunicam da seguinte forma:

1. O navegador envia uma solicitação HTTP para obter informações
2. O server Web se comunica com um server de banco de dados.
3. O servidor Web retorna conteúdo estático, como páginas HTML, imagens, vídeos ou arquivos, em uma resposta HTTP ao navegador.
4. O navegador então exibe as informações para você

Um site que hospeda conteúdo estático, como blogs, imagens de cabeçalho ou artigos, pode ser executado em um servidor Web. No entanto, a maioria dos sites e aplicações da Web são muito mais interativos e exigem um servidor de aplicações.

---
### **2. Servidor de aplicações**

Um servidor de aplicações amplia os recursos de um servidor Web ao oferecer suporte à geração dinâmica de conteúdo, à lógica da aplicação e à integração com vários recursos. Ele fornece um ambiente de runtime onde você pode executar o código da aplicação e interagir com outros componentes de software, como sistemas de mensagens e bancos de dados. 

Quando você tenta acessar conteúdo interativo em um site, o processo funciona da seguinte maneira:

1. O navegador envia uma solicitação HTTP para obter informações
2. O servidor Web transfere a solicitação para o servidor de aplicações
3. O servidor de aplicações aplica a lógica de negócios e se comunica com outros servidores e sistemas de terceiros para atender à solicitação
4. O servidor de aplicações renderiza uma nova página HTML e a retorna como uma resposta ao servidor Web
5. O servidor Web retorna a resposta ao navegador
6. O navegador exibe as informações para você

Para usar o exemplo de um site de comércio eletrônico, ao adicionar itens ao carrinho ou finalizar a compra de itens, você interage com o servidor de aplicações.