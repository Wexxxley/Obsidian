
___

Api é um conjunto de funções e padrões estabelecidos por uma aplicação para que outras aplicações possam utilizar suas funcionalidades sem precisar conhecer detalhes da implementação. 
### **1. Web Service/Web API**
Web Service é um serviço que permite a comunicação entre diferentes aplicações via protocolos da web, geralmente usando JSON. Web services utilizam protocolos padrão da web, como HTTP/HTTPS. Além disso, seguem padrões de formatação e comunicação como o REST.

- **REST(Representational State Transfer):** Utiliza métodos HTTP (GET, POST, PUT, DELETE) e normalmente transmite dados em JSON. 
- **Api vs Web service**: Api é um conceito geral que se refere a uma interface que permite a comunicação entre sistemas. Já Web Service é uma forma específica de API na Web.
- **ASP.NET:** Asp.NET é o framework da Microsoft para criar Web APIs aderentes ao estilo REST na plataforma .NET. Quando uma API adere ao estilo REST ela é chamada de API RESTful.

### **2. Protocolo HTTP**
HTTP (Hypertext Transfer Protocol) é um protocolo de comunicação utilizado na web para a transferência de informações entre clientes e servidores. 

[3_Http e cookies](2_Redes%20de%20computadores/2_Camada%20Aplicação/3_Http%20e%20cookies.md)
  
**Requisição http**
1. Request line (Método HTTP + URI + protocolo HTTP)
2. Headers (Metadados sobre a requisição)
3. Body (Informação opcional enviada ao servidor)

**Resposta http**
4. Status line (Código de status)
5. Headers (Metadados sobre a resposta)
6. Body (Informação opcional enviada ao cliente)

__________________________________________________________________________________

### 1.4 HTTPS E TLS

 HTTPS (Hypertext Transfer Protocol Secure) é uma extensão do HTTP. Enquanto o HTTP transmite dados em texto simples, o que significa que qualquer pessoa interceptando a comunicação pode ler as informações, o HTTPS criptografa os dados transmitidos, protegendo-os contra interceptação. Para implementar HTTPS, o servidor precisa de um certificado TLS. Este certificado autentica a identidade do servidor e permite a criação de uma conexão criptografada.

  

 TLS (Transport Layer Security) é o protocolo de segurança que permite a implementação de HTTPS. O TLS garante que o servidor (e opcionalmente o cliente) seja autenticado, confirmando que ambas as partes são quem dizem ser.

  
  

Você pode adicionar dois middlewares de segurança para a utilização de HTTPS:

- app.UseHttpsRedirection(): Este middleware força as requisições HTTP a serem redirecionadas para HTTPS. Ou seja, se um usuário tentar acessar a aplicação via HTTP, ele será automaticamente redirecionado para a versão HTTPS da URL.
    
- app.UseHsts(): Instrui os navegadores a fazer apenas requisições HTTPS para o servidor, adicionando uma camada extra de segurança contra ataques.
    

**