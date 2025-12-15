
#Concluded 

---
### **1. Servidor Web**

Um servidor web é um computador que armazena arquivos que compõem os sites (HTML, CSS, JavaScript) e os entrega para o dispositivo do usuário final. Está conectado a Internet e pode ser acessado através do seu nome de domínio (DNS), como por exemplo `mozilla.org`.

Para publicar um website, é necessário ou um servidor web estático ou um dinâmico.

- Um **servidor web estático** é chamado "estático" porque o servidor envia seus arquivos tal como foram criados e armazenados ao navegador.

- Um **servidor web dinâmico** consiste em um servidor web estático com software adicional, mais comumente um servidor de aplicações (_application server)_ e um banco de dados (database). É chamado "dinâmico" porque o servidor de aplicações atualiza os arquivos hospedados antes de enviá-los ao navegador através do servidor HTTP.

Sites como a Wikipédia possue vários milhares de páginas web, mas elas não são realmente documentos HTML, mas apenas alguns poucos _templates_ HTML e uma gigantesca base de dados. Essa configuração agiliza e facilita o gerenciamento e a entrega do conteúdo.

---
um servidor web fornece suporte para [HTTP](https://developer.mozilla.org/pt-BR/docs/Glossary/HTTP) (protocolo de transferência de hipertexto). Como o próprio nome indica, o HTTP especifica como transferir arquivos de hipertexto (ou seja, documentos vinculados da web) entre dois computadores.

Um _protocolo_ é um conjunto de regras para comunicação entre dois computadores. HTTP é um protocolo textual sem estado.

[Textual](https://developer.mozilla.org/pt-BR/docs/Learn_web_development/Howto/Web_mechanics/What_is_a_web_server#textual)

Todos os comandos são de texto simples e legíveis por humanos.

[Sem estado](https://developer.mozilla.org/pt-BR/docs/Learn_web_development/Howto/Web_mechanics/What_is_a_web_server#sem_estado)

Nem o servidor nem o cliente lembram de comunicações anteriores. Por exemplo, confiando apenas no HTTP, um servidor não consegue se lembrar de uma senha digitada ou da etapa em que você está em uma transação. Você precisa de um servidor de aplicativos para tarefas como essa. (Nós vamos cobrir esse tipo de tecnologia em mais artigos.)

O HTTP fornece regras claras sobre como um cliente e um servidor se comunicam. Abordaremos o próprio HTTP em um artigo técnico mais adiante. Por enquanto, apenas fique atento a estas coisas:

- Somente _clientes_ podem fazer requisições HTTP, e somente para _servidores._ Servidores podem apenas _responder_ a uma requisição HTTP dos _clientes_.
- Quando fizer a requisição de um arquivo via HTTP, os clientes devem fornecer a [URL](https://developer.mozilla.org/pt-BR/docs/Glossary/URL) do arquivo.
- O servidor web _deve responder_ todas as requisições HTTP, mesmo que seja com uma mensagem de erro.

[  
](https://developer.mozilla.org/en-US/404)




O Servidor Web é otimizado para **entrega rápida** de dados brutos e estáticos. Ele atua como a camada de front-end e interface de rede.

- É projetado para servir **conteúdo estático**, como arquivos HTML, CSS, JavaScript, imagens e vídeos.
    
- Utiliza primariamente **HTTP** e **HTTPS**. Em menor grau, pode suportar **FTP** e **SMTP**.
    
- Lida com solicitações HTTP e roteamento básico. Sua execução envolve pouca lógica de negócios; seu foco é na eficiência de I/O.
    
- Pode atuar como um **Proxy Reverso**, lidando com a terminação SSL/TLS e encaminhando apenas solicitações complexas para o Servidor de Aplicações.    

- O Servidor Web não precisa de uma JVM ou CLR. Ele é geralmente escrito em linguagens de baixo nível (como C/C++). Seu runtime é focado na eficiência de I/O

---
### **2. Servidor de Aplicações**

O Servidor de Aplicações é a plataforma de back-end onde a lógica de negócio complexa é executada.

- É responsável por gerar **conteúdo dinâmico** em tempo real, que é o resultado de uma computação (ex: o saldo bancário de um usuário, a lista de itens em um carrinho de compras). Esse conteúdo não existe como um arquivo.
    
- O Servidor de Aplicações **precisa** de um ambiente de runtime completo (como a **JVM** ou o **.NET CLR**) porque seu trabalho é gerenciar a lógica de negócios e o estado complexo. 
    
- Executa a **lógica de negócios** e lida com processamento intensivo de recursos. Suas tarefas incluem gerenciamento de sessões, gerenciamento de transações (ACID).
    
- Suporta uma gama mais ampla de protocolos (como RMI, RPC, ou protocolos de mensagem) para se integrar a sistemas e serviços corporativos, além de HTTP.
    

---
### **3. A Separação Arquitetural**

Em um ambiente empresarial de alto desempenho, os dois servidores trabalham em conjunto:

1. O **Servidor Web** recebe todas as requisições de Aplicação.
    
2. Ele **interpreta** a requisição. Se for um arquivo estático, ele entrega diretamente.
    
3. Se a requisição for para conteúdo dinâmico, o Servidor Web a encaminha para o **Servidor de Aplicações**.
    
4. O Servidor de Aplicações gera o conteúdo dinâmico e o envia de volta ao Servidor Web, que o empacota e o devolve ao cliente.
    
