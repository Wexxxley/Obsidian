
---

A ideia central é organizar as classes ou módulos em **camadas** dispostas de forma **hierárquica**.

**Regra Principal de Dependência:**
- Uma camada só pode usar os serviços (chamar métodos, instanciar objetos, etc.) da camada **imediatamente inferior** a ela. Ela não pode "pular" camadas nem acessar camadas superiores.
    



- Por exemplo, a pilha de protocolos da Internet segue essa estrutura:
    
    - Camada de Aplicação (ex: HTTP) usa serviços da...
        
    - Camada de Transporte (ex: TCP) que usa serviços da...
        
    - Camada de Rede (ex: IP) que usa serviços da...
        
    - Camada de Enlace/Física (ex: Ethernet) 5.
        

**Vantagens:**

- **Particiona a Complexidade:** Divide um sistema complexo em partes menores e mais gerenciáveis (as camadas)6.
    
- **Disciplina as Dependências:** A regra de dependência estrita (só usar a camada inferior) ajuda a organizar o sistema e facilita o entendimento, a manutenção e a evolução 7.
    
- **Facilita a Substituição:** Torna mais fácil trocar a implementação de uma camada sem afetar as camadas superiores (desde que a interface seja mantida). Ex: Mudar de TCP para UDP na camada de transporte8.
    
- **Promove o Reúso:** Camadas inferiores podem ser reutilizadas por múltiplas camadas superiores. Ex: Vários protocolos de aplicação (HTTP, SMTP, FTP) podem usar a mesma camada de transporte (TCP) 9.
    

**Aprofundamento (Contexto Histórico):**

- Uma das primeiras propostas de arquitetura em camadas foi feita por Edsger Dijkstra em 1968 para o sistema operacional THE10. As camadas iam desde multiprogramação (nível 0) até os programas dos usuários (nível 4)11. Dijkstra já destacava os benefícios dessa estrutura hierárquica, especialmente para projetos grandes12.
    

Próximo Passo: Arquitetura em Três Camadas

Agora que entendemos o conceito geral, vamos ver uma aplicação muito comum dessa arquitetura: a Arquitetura em Três Camadas, frequentemente usada em sistemas de informação corporativos.

Quando quiser continuar, é só digitar "next".

![](attachments/Pasted%20image%2020251023202231.png)