

---

Um **firewall** é uma combinação de hardware e software que isola a rede interna de uma organização da Internet em geral. Ele atua como um guarda de segurança, permitindo que alguns pacotes passem e bloqueando outros, com base em regras de segurança definidas pelo administrador da rede.

![600](../../attachments/Pasted%20image%2020251215191721.png)

### **1. Tipos de Firewalls**

1. **Filtros de Pacotes Tradicionais**
    - Inspecionam cada datagrama isoladamente à medida que passam pelo roteador.
    - As decisões de bloquear ou permitir são baseadas em informações do cabeçalho, como endereços IP de origem/destino, tipo de protocolo (TCP/UDP), portas de origem/destino e flags TCP.
    - Exemplo: Um administrador pode configurar o firewall para bloquear todos os pacotes UDP que chegam.
        
2. **Filtros de Pacote com Controle de Estado:**
    - Eles não olham apenas para o pacote isolada. Eles mantêm uma tabela de conexões para saber se um pacote que está chegando faz parte de uma comunicação já estabelecida e legítima. Isso impede, por exemplo, que um atacante envie pacotes maliciosos que pareçam respostas a conexões internas que nunca foram solicitadas.
        
3. **Gateways de Aplicação (Application Gateways):**
    - Para usar um serviço externo (como Telnet ou FTP), o usuário interno se conecta primeiro ao gateway de aplicação. O gateway verifica as credenciais do usuário e, se permitido, estabelece a conexão com o destino externo em nome do usuário, agindo como um intermediário. Isso permite, por exemplo, autorizar o uso de Telnet apenas para um grupo específico de funcionários4.    

---
### **2. Onde o firewall é aplicado?**

- **Proxy reverso:** Na prática moderna, o firewall do tipo Application gateway é frequentemente implementado como um Proxy Reverso (WAF - _Web Application Firewall_).
        
-  **Roteadores de Borda:** Usando filtragem de pacotes (baseada apenas em IP e porta, sem ler o conteúdo da mensagem).
        
- **Sistemas Finais:** Diretamente no sistema operacional.

---
### **3. Firewall corporativo e pessoal**

- **Firewall Corporativo:** Geralmente hardwares dedicados ou softwares complexos em roteadores que protegem milhares de máquinas de uma vez.
    
- **Firewall Pessoal:** É um software instalado diretamente no computador do usuário comum.
	- Ex: O **Windows Defender Firewall** que já vem no Windows.
