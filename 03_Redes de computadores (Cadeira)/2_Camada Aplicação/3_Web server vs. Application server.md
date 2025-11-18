
#Concluded 

---
### **1. Servidor Web**

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
    
