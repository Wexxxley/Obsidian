


---
### **Como funciona um servidor Web**

Um servidor Web é uma tecnologia que hospeda o código e os dados de um site. Quando você insere um URL no seu navegador, o URL é, na verdade, o identificador de endereço do servidor Web.

Seu navegador e servidor Web se comunicam da seguinte forma:

1. O navegador usa o URL para encontrar o endereço IP do servidor
2. O navegador envia uma solicitação HTTP para obter informações
3. O servidor Web se comunica com um servidor de banco de dados para encontrar os dados relevantes
4. O servidor Web retorna conteúdo estático, como páginas HTML, imagens, vídeos ou arquivos, em uma resposta HTTP ao navegador
5. O navegador então exibe as informações para você

Um site que hospeda conteúdo estático, como blogs, imagens de cabeçalho ou artigos, pode ser executado em um servidor Web. No entanto, a maioria dos sites e aplicações da Web são muito mais interativos e exigem um servidor de aplicações.

### **Como funciona um servidor de aplicações**

Um servidor de aplicações amplia os recursos de um servidor Web ao oferecer suporte à geração dinâmica de conteúdo, à lógica da aplicação e à integração com vários recursos. Ele fornece um ambiente de runtime onde você pode executar o código da aplicação e interagir com outros componentes de software, como sistemas de mensagens e bancos de dados. Ele usa a lógica de negócios para transformar dados de forma mais significativa do que um servidor Web.

Quando você tenta acessar conteúdo interativo em um site, o processo funciona da seguinte maneira:

1. O navegador usa a URL para encontrar o endereço IP do servidor
2. O navegador envia uma solicitação HTTP para obter informações
3. O servidor Web transfere a solicitação para o servidor de aplicações
4. O servidor de aplicações aplica a lógica de negócios e se comunica com outros servidores e sistemas de terceiros para atender à solicitação
5. O servidor de aplicações renderiza uma nova página HTML e a retorna como uma resposta ao servidor Web
6. O servidor Web retorna a resposta ao navegador
7. O navegador exibe as informações para você

Para usar o exemplo de um site de comércio eletrônico, ao adicionar itens ao carrinho ou finalizar a compra de itens, você interage com o servidor de aplicações.