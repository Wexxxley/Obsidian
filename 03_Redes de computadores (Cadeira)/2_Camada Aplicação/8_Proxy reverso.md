


---
### **1. Proxy reverso**

Um servidor real não expõe suas aplicações diretamente à internet. Em vez disso, você usa um Proxy Reverso como o único "porteiro". Neste cenário, apenas o Proxy Reverso escuta na porta 80.

Vamos supor que duas aplicações HTTP rodam internamente, em portas diferentes (ex: `localhost:3000` e `localhost:8080`), inacessíveis pela internet.

1. O usuário acessa `http://meuservidor.com` (porta 80)    
2. O Proxy Reverso recebe a requisição. E inspeciona a requisição HTTP, geralmente o nome de domínio.
3. Ele usa regras de roteamento que você definiu:
    - Se o usuário pediu `http://app1.meuservidor.com`,  ele encaminha a requisição para App1.
    - Se o usuário pediu `http://app2.meuservidor.com`, ele encaminha a requisição para App2.
        
Para o usuário final, ambas as aplicações parecem estar rodando na porta 80, mas em domínios diferentes. A complexidade das portas internas (`:3000`, `:8080`) fica totalmente escondida do usuário. É assim que um único servidor pode hospedar centenas de sites diferentes usando um único endereço IP.
