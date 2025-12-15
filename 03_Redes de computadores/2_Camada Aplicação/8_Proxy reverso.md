
#Concluded 

---
### **1. E se um server rodar duas aplicações http (mesma porta)?**

Um servidor real não expõe suas aplicações diretamente à internet. Em vez disso, você usa um Proxy Reverso como o único "porteiro". Neste cenário, apenas o Proxy Reverso escuta na porta 80.

Vamos supor que duas aplicações HTTP rodam internamente, em portas diferentes (ex: `localhost:3000` e `localhost:8080`), inacessíveis pela internet.

1. O usuário acessa `http://meuservidor.com` (porta 80)    
2. O Proxy Reverso recebe a requisição. E inspeciona a requisição HTTP, geralmente o nome de domínio.
3. Ele usa regras de roteamento que você definiu:
    - Se o usuário pediu `http://app1.meuservidor.com`,  ele encaminha a requisição para App1.
    - Se o usuário pediu `http://app2.meuservidor.com`, ele encaminha a requisição para App2.
        
Para o usuário final, ambas as aplicações parecem estar rodando na porta 80, mas em domínios diferentes. A complexidade das portas internas (`:3000`, `:8080`) fica totalmente escondida do usuário. É assim que um único servidor pode hospedar centenas de sites diferentes usando um único endereço IP.

![](../../attachments/Pasted%20image%2020251215190915.png)

---
### **2. Outras Funções de um Proxy Reverso**

1. **Balanceamento de Carga :** Esta é talvez a sua função mais importante. Em vez de `app1.meuservidor.com` apontar para uma única aplicação, ele pode apontar para um grupo de servidores idênticos que rodam a `App1`. O proxy reverso distribui as requisições recebidas entre esses servidores, evitando que um único servidor fique sobrecarregado. 
    
2. **Terminação SSL/TLS:** Suas aplicações internas (como `App1` e `App2`) não precisam saber lidar com criptografia (HTTPS). Elas podem rodar em HTTP simples (porta `:3000`, `:8080`). O proxy reverso fica na frente, escutando na porta 443 (HTTPS), e assume 100% do trabalho de descriptografar a requisição do usuário, enviá-la em HTTP para a aplicação interna e, em seguida, criptografar a resposta de volta para o usuário. 
    
3. **Caching de Conteúdo Estático:** O proxy reverso pode armazenar em cache arquivos que não mudam com frequência, como imagens (`.png`), arquivos de estilo (`.css`) e scripts (`.js`). 
    
4. **Segurança e WAF (Web Application Firewall):** Como todo o tráfego passa por ele, o proxy reverso é o local ideal para filtrar tráfego malicioso. Você pode instalar um **WAF** nele para bloquear automaticamente ataques comuns.