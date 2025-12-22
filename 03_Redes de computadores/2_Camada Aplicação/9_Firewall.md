
#Concluded 

---
### **1. Definição**

O firewall é uma barreira de segurança essencial que isola a rede interna (confiável) da Internet (não confiável).

Atua como um "porteiro", controlando o tráfego nas portas de comunicação. Ele permitir a passagem de pacotes autorizados e bloquea os não autorizados com base em regras predefinidas. Ele impede tanto a entrada de invasores quanto a saída de dados por malwares.

![600](../../attachments/Pasted%20image%2020251215191721.png)

---
### **2. Classificação: Hardware vs. Software**

Podemos classificar o firewall primeiramente pelo que ele _é_ fisicamente:

- **Firewall de Hardware:** É um equipamento físico dedicado, podendo ser um dispositivo específico ou um roteador com firewall integrado. Geralmente utilizado em grandes corporações para lidar com alto volume de tráfego. São soluções mais caras.
        
- **Firewall de Software:** É um programa instalada no sistema operacional de um computador ou celular. Comum em dispositivos pessoais e servidores individuais.

---
### **3. Métodos de Filtragem**

Independentemente de ser hardware ou software, o firewall utiliza diferentes lógicas para inspecionar os dados. 

1. **Filtros de Pacotes Tradicionais (Stateless):**
    - Inspecionam cada pacote **isoladamente**.
    - Tomam decisões simples baseadas apenas no cabeçalho (IP origem/destino, Porta, Protocolo TCP/UDP).
    - Exemplo: "Bloquear todos os pacotes UDP vindos da porta 53".
        
2. **Filtros de Pacote com Controle de Estado (Stateful):**
    - Mais inteligentes, eles mantêm uma **tabela de conexões**.
    - Eles sabem o contexto: "Este pacote que está chegando é uma resposta a um pedido que saiu daqui de dentro?". Se não for, ele bloqueia, impedindo ataques que tentam se disfarçar de respostas legítimas.
        
3. **Gateways de Aplicação (Application Gateways):**
    - Atuam como intermediários (**Proxies**) específicos para uma aplicação.
    - O usuário conecta no Gateway, que verifica credenciais e conteúdo antes de conectar ao destino final. É uma inspeção profunda do conteúdo, não apenas do cabeçalho.

---
### **4. Escopo de Proteção: Corporativo vs. Pessoal**

- **Firewall de Rede (Corporativo):**
    - **Onde fica:** Na borda da rede (roteadores de entrada).
    - **Quem protege:** Protege **todos** os computadores daquela rede simultaneamente.
        
- **Firewall Pessoal:**
    - **Onde fica:** Instalado diretamente no dispositivo final (ex: _Windows Defender_ no seu PC).
    - **Quem protege:** Apenas a máquina específica.

---
### **5. Aplicação Prática e Localização**

Na arquitetura de redes moderna, os firewalls são aplicados em camadas:

- **Nos Roteadores de Borda:** Fazem a filtragem grossa baseada em IP e porta.
    
- **No Proxy Reverso (WAF):** O conceito de _Application Gateway_ moderno. Ele fica na frente dos servidores Web protegendo as aplicações contra ataques complexos.
    
- **Nos Sistemas Finais:** A última linha de defesa no próprio sistema operacional.

