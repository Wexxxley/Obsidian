

---

Um **firewall** é uma combinação de hardware e software que isola a rede interna de uma organização da Internet em geral. Ele atua como um guarda de segurança, permitindo que alguns pacotes passem e bloqueando outros, com base em regras de segurança definidas pelo administrador da rede.

![600](../../attachments/Pasted%20image%2020251215191721.png)

### **1. Tipos de Firewalls**

- **Firewall de Hardware:** É um equipamento físico dedicado, "palpável".
    
    - Pode ser um dispositivo específico (que parece um switch ou roteador) ou um roteador que possui a função de firewall integrada.
        
    - Geralmente é mais caro (o vídeo cita valores altos para equipamentos corporativos de ponta) e usado para lidar com grande volume de tráfego.
        
- **Firewall de Software:** É um programa instalado no seu dispositivo (computador ou celular).
    
    - Não é uma peça física separada, mas sim uma aplicação rodando no seu sistema operacional.

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
    
- **Firewall Pessoal:** É um software instalado diretamente no computador do usuário comum. Assim como um porteiro controla quem entra e sai pela, o firewall controla os dados que entram e saem pelas "portas" de comunicação do seu computador ou rede.
	- Ex: O **Windows Defender Firewall** que já vem no Windows.

- **Firewall de Rede:**
    
    - Fica posicionado na entrada da rede.
        
    - **Protege todos:** Ele filtra o tráfego para _todos_ os computadores conectados àquela rede. Se algo é bloqueado ali, não chega a ninguém.
        
- **Firewall Pessoal:**
    
    - É instalado individualmente em cada computador (como o Firewall do Windows).
        
    - **Proteção Individual:** Ele protege apenas a máquina onde está instalado. O vídeo dá o exemplo: se você tem o firewall ativado no seu PC, você está seguro; se o colega do lado, na mesma rede, não tiver um firewall pessoal ativado na máquina dele, ele _não_ está protegido, mesmo estando ao seu lado.

Além de apenas bloquear, o firewall **monitora o comportamento** do tráfego.

- **Detecção de Anomalias:** Se uma porta que costuma ter pouco tráfego (ex: 2 conexões por minuto) de repente recebe 400 conexões simultâneas, o firewall percebe que algo está errado.
    
- **Aviso ao Administrador:** Ele gera alertas para o gerente de rede investigar, pois isso pode indicar um ataque ou uma máquina infectada tentando se espalhar.
    

#### 3. O que o Firewall NÃO faz (Muito Importante!)

O vídeo enfatiza um ponto que costuma ser "pegadinha" em provas e confusão comum:

- **Não remove vírus:** O firewall é um guarda de fronteira, não um médico. Se o vírus _já está_ dentro do seu computador, o firewall não vai removê-lo ou consertar o sistema.
    
- **Contenção:** O máximo que ele pode fazer nesse caso é impedir que esse vírus se comunique com o hacker externo (bloqueando a saída), mas o vírus continuará instalad




### **1. Definição e Conceito Fundamental**

O **firewall** é uma barreira de segurança essencial que isola a rede interna (confiável) da Internet (não confiável).

- **Função:** Atua como um "porteiro", controlando o tráfego nas portas de comunicação.
    
- **Objetivo:** Permitir a passagem de pacotes autorizados e bloquear os não autorizados com base em regras predefinidas. Ele impede tanto a entrada de invasores quanto a saída de dados por malwares (como backdoors tentando se comunicar com hackers).

### **2. Classificação: Hardware vs. Software**

Podemos classificar o firewall primeiramente pelo que ele _é_ fisicamente:

- **Firewall de Hardware:** É um equipamento físico dedicado, podendo ser um dispositivo específico ou um roteador com firewall integrado. Geralmente utilizado em grandes corporações para lidar com alto volume de tráfego. São soluções mais caras.
        
- **Firewall de Software:** É uma aplicação programa instalada no sistema operacional de um computador ou celular.
        
    - _Uso:_ Comum em dispositivos pessoais e servidores individuais.
        

### 3. Métodos de Filtragem (Como ele decide bloquear?)

Independentemente de ser hardware ou software, o firewall utiliza diferentes lógicas para inspecionar os dados. O livro detalha três níveis de sofisticação:

1. **Filtros de Pacotes Tradicionais (Stateless):**
    
    - Inspecionam cada pacote **isoladamente**.
        
    - Tomam decisões simples baseadas apenas no cabeçalho (IP origem/destino, Porta, Protocolo TCP/UDP).
        
    - _Exemplo:_ "Bloquear todos os pacotes UDP vindos da porta 53".
        
2. **Filtros de Pacote com Controle de Estado (Stateful):**
    
    - Mais inteligentes, eles mantêm uma **tabela de conexões**.
        
    - Eles sabem o contexto: "Este pacote que está chegando é uma resposta a um pedido que saiu daqui de dentro?". Se não for, ele bloqueia, impedindo ataques que tentam se disfarçar de respostas legítimas.
        
3. **Gateways de Aplicação (Application Gateways):**
    
    - Atuam como intermediários (**Proxies**) específicos para uma aplicação (como Telnet, FTP ou HTTP).
        
    - O usuário conecta no Gateway, que verifica credenciais e conteúdo antes de conectar ao destino final. É uma inspeção profunda do conteúdo, não apenas do cabeçalho.
        

### 4. Escopo de Proteção: Corporativo vs. Pessoal

Onde o firewall protege e quem ele cobre?

- **Firewall de Rede (Corporativo):**
    
    - **Onde fica:** Na borda da rede (roteadores de entrada).
        
    - **Quem protege:** Protege **todos** os computadores daquela rede simultaneamente. Se a ameaça é barrada aqui, ela não chega a ninguém.
        
- **Firewall Pessoal (Host-based):**
    
    - **Onde fica:** Instalado diretamente no dispositivo final (ex: _Windows Defender_ no seu PC).
        
    - **Quem protege:** Apenas a máquina específica.
        
    - _Cenário:_ Se você tem um firewall pessoal e seu colega ao lado (na mesma rede) não tem, você está seguro, mas ele está vulnerável.
        

### 5. Aplicação Prática e Localização

Na arquitetura de redes moderna, os firewalls são aplicados em camadas:

- **Nos Roteadores de Borda:** Fazem a filtragem grossa (Stateless/Stateful) baseada em IP e porta.
    
- **No Proxy Reverso (WAF):** O conceito de _Application Gateway_ moderno. Ele fica na frente dos servidores Web protegendo as aplicações contra ataques complexos.
    
- **Nos Sistemas Finais:** A última linha de defesa no próprio sistema operacional.
    

### 6. Monitoramento e Limitações (O que ele faz e o que NÃO faz)

**O que ele faz além de bloquear:**

- **Monitoramento de Comportamento:** Detecta anomalias. Por exemplo, se uma porta que costuma ter 2 conexões/minuto de repente recebe 400, o firewall percebe o padrão suspeito.
    
- **Alertas:** Gera logs e avisos para o administrador investigar possíveis ataques ou infecções.
    

**O que ele NÃO faz (Importante!):**

- **Não é Antivírus:** O firewall é um "guarda de fronteira", não um "médico".
    
- **Não remove vírus existentes:** Se um malware já entrou (por um pendrive ou download autorizado pelo usuário), o firewall não consegue removê-lo do sistema. Ele pode, no máximo, tentar impedir que esse vírus envie dados para fora (contenção de saída).