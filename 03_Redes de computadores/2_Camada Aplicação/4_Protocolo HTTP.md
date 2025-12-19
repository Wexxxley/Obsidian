
#Concluded 

___
### **1. HTTP**

O HTTP (_Hypertext Transfer Protocol_) é um <mark style="background: #ADCCFFA6;">protocolo que padroniza a troca de dados na Web seguindo o modelo cliente-servidor e operando sobre o TCP</mark> através de ciclos de requisição e resposta.
- O Cliente (browser) solicita, o servidor envia os objetos e o browser os apresenta.
- É stateless, tratando cada interação como independente e não guardando memória das requisições anteriores.

**Response message**
![500](../../attachments/Pasted%20image%2020250508160317.png)
**Com método get**
![450](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcyujfV7oaza6FHi6b0fL9V616AIvE9KT8DGsxOrcc9auf5umHYGcpG8YT5CpaVU7Ml3cGPQxCXnbauDhgefOwtUQMica6ZF6Qvy5Vtyjrxf3GTU1uDd-lDp1GaKeklK6J4JpJXPQ?key=HrOhHC0_-ked6RNCpQ0o3PZn)

**Com método Put**
![320](https://lh7-rt.googleusercontent.com/docsz/AD_4nXewOFt0a4Pe9a_5Jo1JgCrozaMzTDvK4zXIbQdGsfDauSrPLBQN5OCLhJEeFem7rr4NjGIK0r1sZkbSTCFTwMUYLUY9xiZMyrB3LMb99NEQRvZ2U1vBg3W0GHF50JswLKLsNO38TA?key=HrOhHC0_-ked6RNCpQ0o3PZn)

**Formato do Response message**
![550](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfDmPpFdskH2rw36i9oGJ_mKfY4EdYbALCl6NvQtc_jrz6STrJsxdzjVKpxRH69sFsQIn09EY3XTyB6Rg3Ke9o4eNQhU_tsXHMt4zaXT_Jb8IHOHjgI496KzWLulyo8yjhOIqBOdg?key=HrOhHC0_-ked6RNCpQ0o3PZn)


**Códigos de status**: São códigos utilizados nas respostas http para informar ao cliente se a requisição foi bem sucedida, se ocorreu algum erro, etc.

O primeiro dígito do código de status define a classe de resposta. Os dois últimos dígitos não têm nenhuma função de categorização. Existem cinco valores para o primeiro dígito:

- 1xx (Informacional): Resposta provisória - a solicitação foi recebida, continuando o processo.
- 2xx (Bem-sucedido)](https://learn.microsoft.com/en-us/troubleshoot/developer/webapps/iis/health-diagnostic-performance/http-status-code#2xx---successful): O servidor recebeu e aceitou a solicitação com sucesso.
- [3xx (Redirecionamento)](https://learn.microsoft.com/en-us/troubleshoot/developer/webapps/iis/health-diagnostic-performance/http-status-code#3xx---redirection): Mais medidas precisam ser tomadas para concluir a solicitação.
- [4xx (Erro do cliente)](https://learn.microsoft.com/en-us/troubleshoot/developer/webapps/iis/health-diagnostic-performance/http-status-code#4xx---client-error): A solicitação contém um erro e não pode ser atendida.
- [5xx (Erro do servidor)](https://learn.microsoft.com/en-us/troubleshoot/developer/webapps/iis/health-diagnostic-performance/http-status-code#5xx---server-error): O servidor não conseguiu atender à solicitação.

#### **1.1 HTTP Persistente**
Técnica onde a mesma conexão TCP é reutilizada para enviar vários pedidos HTTP, em vez de abrir uma nova conexão para cada requisição. Esee é o padrão desde 1997. 

Precisamos lembrar que o TCP exige um Handshake de 3 vias para começar e outro processo para terminar. Isso gasta tempo.

1. **HTTP Não Persistente:**
    - Imagine que você entra em um site que tem 10 imagens.
    - O navegador abre uma conexão TCP -> Baixa o HTML -> Fecha a conexão.
    - Abre _nova_ conexão TCP -> Baixa imagem 1 -> Fecha.
    - Abre _nova_ conexão TCP -> Baixa imagem 2 -> Fecha.
        
2. **HTTP Persistente:**
    - O navegador abre uma conexão TCP -> Baixa o HTML.
    - A conexão permanece aberta (Keep-Alive).
    - Pela _mesma_ conexão, ele baixa a imagem 1, a imagem 2, o CSS, etc.
    - Só fecha a conexão após um tempo de inatividade ou quando tudo for baixado.

---
### **2. HTTPS e TLS**

Enquanto o HTTP transmite dados em texto simples, o que significa que qualquer pessoa interceptando a comunicação pode ler as informações, o<mark style="background: #ADCCFFA6;"> HTTPS criptografa os dados transmitidos, protegendo-os contra interceptação</mark>. Para implementar HTTPS, o servidor precisa de um certificado TLS. Este certificado autentica a identidade do servidor e permite a criação de uma conexão criptografada.

**TLS (Transport Layer Security)** é o protocolo de segurança que permite a implementação de HTTPS. O TLS garante que o servidor (e opcionalmente o cliente) seja autenticado, confirmando que ambas as partes são quem dizem ser.
