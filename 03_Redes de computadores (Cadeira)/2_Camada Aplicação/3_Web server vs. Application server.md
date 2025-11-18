
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

---
### **3. Diferenças**

**Tarefas abrangidas**
- Um servidor Web hospeda sites e fornece respostas a solicitações simples. Os servidores Web também registram a atividade do servidor e permitem scripts no lado do servidor.

- Por outro lado, os servidores de aplicações têm um conjunto de tarefas mais complexo. Os servidores de aplicações lidam com a lógica de negócios para gerar conteúdo dinâmico por meio da conexão com sistemas, serviços e bancos de dados corporativos.
### **Protocolos usados**

O protocolo primário que os servidores Web usam é o protocolo HTTP. No entanto, diferentes servidores Web também oferecem suporte a FTP e Simple Mail Transfer Protocol (SMTP).

Além dos protocolos que os servidores Web usam, os servidores de aplicações usam protocolos de comunicação adicionais para se comunicar com outros componentes de software. Por exemplo, eles podem usar Remote Method Invocation (RMI – Invocação de método remoto) e Remote Procedure Call (RPC – Chamada de procedimento remoto).

### **Tipos de conteúdo**

Os servidores Web geralmente fornecem conteúdo estático. Conteúdo estático é conteúdo que um servidor não precisa modificar ou processar antes de entregar. Por exemplo, arquivos de imagem (como PNG, GIF e JPEG), documentos para download (PDFs), vídeos e arquivos HTML são todos conteúdo estático. 

Os servidores de aplicações geralmente fornecem conteúdo dinâmico. O conteúdo dinâmico é aquele que muda com base na forma como o usuário interage com ele. Por exemplo, relatórios gerados dinamicamente, representações de dados personalizadas, interfaces de usuário personalizadas, resultados de banco de dados e HTML processado são todos conteúdos dinâmicos.

### **Multithreading**

Os threads em um servidor são caminhos de operação separados que permitem o processamento simultâneo de tarefas. No multithreading, o servidor cria e executa vários encadeamentos simultaneamente, e cada um lida com uma tarefa separada ou parte de uma tarefa. O suporte para multithreading ajuda a fornecer conteúdo da Web com mais rapidez e, ao mesmo tempo, gerenciar mais tráfego na Web.

A maioria dos servidores Web não é compatível com multithreading. Os servidores Web colocam cada nova solicitação de conexão em uma fila e usam um loop de eventos para monitorar novas entradas e saídas da fila. Para melhorar a eficiência, o servidor processa as solicitações usando E/S e retornos de chamada sem bloqueio. Operações sem bloqueio e arquitetura orientada por eventos permitem que os servidores Web lidem com conexões simultâneas.

Os servidores de aplicações usam multithreading para fornecer alta escalabilidade e eficiência. Se uma solicitação exigir recursos externos, o servidor de aplicações usará segmentos separados para cobrir essas interações. Ele pode processar vários segmentos ao mesmo tempo, atendendo a várias interações com clientes em paralelo. 

## Como os servidores de aplicações e os servidores Web funcionam juntos?

Servidores de aplicações e servidores Web trabalham juntos para lidar com as solicitações dos clientes e fornecer o conteúdo correto ao usuário. O servidor Web sempre recebe uma nova solicitação primeiro. Se ele puder produzir as informações por si só, ele o fará e enviará de volta uma resposta HTTP. Ele também verifica se os dados solicitados pelo usuário ainda não estão no cache.

Se o servidor Web não conseguir acessar o conteúdo de que o usuário precisa, ele encaminha a solicitação ao servidor de aplicações. O servidor de aplicações processa os dados e usa a lógica de negócios para fornecer as informações corretas. Em seguida, ele passa a solicitação de volta para o servidor Web, que a repassa para o usuário. Em certas arquiteturas, você também pode configurar servidores de aplicações para lidar com solicitações HTTP sozinhos.