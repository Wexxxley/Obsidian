
#Concluded 

___
### **1. HTTP**

Protocolo da camada de aplicação da Web. Usa o modelo cliente/servidor.
- O Cliente (browser) solicita, o servidor envia os objetos e o browser os apresenta.
- Protocolo “sem estado”, o servidor não mantém informação sobre os pedidos passados.
- Utiliza o protocolo de transporte TCP.

**HTTP Persistente:** técnica onde a mesma conexão TCP é reutilizada para enviar vários pedidos HTTP, em vez de abrir uma nova conexão para cada requisição. Antes o HTTP era não persistente, a cada requisição o navegador abria uma conexão TCP.

#### **1.1 Formato do Request e response message**

**Response message**
![Pasted image 20250508160317](../../attachments/Pasted%20image%2020250508160317.png)
- CR(Carriage return): retorno do cursor.
- LF(Line Feed): Pula a linha.
- SP(Space): espaço em branco.

**Com método get**
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcyujfV7oaza6FHi6b0fL9V616AIvE9KT8DGsxOrcc9auf5umHYGcpG8YT5CpaVU7Ml3cGPQxCXnbauDhgefOwtUQMica6ZF6Qvy5Vtyjrxf3GTU1uDd-lDp1GaKeklK6J4JpJXPQ?key=HrOhHC0_-ked6RNCpQ0o3PZn)

**Com método Put**
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXewOFt0a4Pe9a_5Jo1JgCrozaMzTDvK4zXIbQdGsfDauSrPLBQN5OCLhJEeFem7rr4NjGIK0r1sZkbSTCFTwMUYLUY9xiZMyrB3LMb99NEQRvZ2U1vBg3W0GHF50JswLKLsNO38TA?key=HrOhHC0_-ked6RNCpQ0o3PZn)

**Formato do Response message**
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfDmPpFdskH2rw36i9oGJ_mKfY4EdYbALCl6NvQtc_jrz6STrJsxdzjVKpxRH69sFsQIn09EY3XTyB6Rg3Ke9o4eNQhU_tsXHMt4zaXT_Jb8IHOHjgI496KzWLulyo8yjhOIqBOdg?key=HrOhHC0_-ked6RNCpQ0o3PZn)

**Códigos de status**
São códigos utilizados nas respostas http para informar ao cliente se a requisição foi bem sucedida, se ocorreu algum erro, etc.
- **200 OK:** requisição bem-sucedida e a informação é entregue com a resposta. 
- **400 Bad Request:** código genérico de erro. 
- **404 Not Found:** o documento requisitado não existe no servidor. 
- **505 HTTP Version Not Supported:** a versão do protocolo HTTP  não suportada pelo servidor.

---
### **2. HTTPS E TLS**

Enquanto o HTTP transmite dados em texto simples, o que significa que qualquer pessoa interceptando a comunicação pode ler as informações, o<mark style="background: #ADCCFFA6;"> HTTPS criptografa os dados transmitidos, protegendo-os contra interceptação</mark>. Para implementar HTTPS, o servidor precisa de um certificado TLS. Este certificado autentica a identidade do servidor e permite a criação de uma conexão criptografada.

**TLS (Transport Layer Security)** é o protocolo de segurança que permite a implementação de HTTPS. O TLS garante que o servidor (e opcionalmente o cliente) seja autenticado, confirmando que ambas as partes são quem dizem ser.

---
### **3. HTTP Cache**

### Parte 1: Visão Geral e Vantagens do Cache HTTP

O **cache HTTP** é um mecanismo essencial que armazena uma resposta associada a uma solicitação e a reutiliza para solicitações subsequentes. A correta operação do cache é fundamental para a integridade e eficiência do sistema.

#### 1.1. Funcionamento e Benefícios

A **reutilização** de respostas armazenadas apresenta várias vantagens funcionais:

1. **Latência Reduzida:** A resposta é entregue mais rapidamente, pois a solicitação não precisa ser roteada ao servidor de origem. Quanto mais próximos o cliente e o cache estiverem, mais rápida será a resposta. O exemplo típico é o cache armazenado no próprio navegador.
    
2. **Redução da Carga do Servidor de Origem:** Quando uma resposta é reutilizável, o servidor de origem não precisa processar a solicitação. Isso significa que não há necessidade de:
    
    - Analisar e rotear a requisição.
        
    - Restaurar a sessão com base no _cookie_.
        
    - Consultar o banco de dados.
        
    - Renderizar o mecanismo de modelo (_template engine_).
        
    - Consequentemente, a carga computacional no servidor é reduzida.
        

---

Aguardando `next` para a explicação dos Tipos de Caches.
