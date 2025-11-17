
#Concluded 

___
### **1. Arquitetura TCP/IP**

<mark style="background: #ADCCFFA6;">A arquitetura TCP/IP é um conjunto de protocolos de comunicação que permite a troca de dados entre dispositivos em uma rede</mark>. 
![500](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfm0yiF7VCzT2a3-JAYru0-quEMlNGUffyxN3fS5Fw5FcE-dLzkcmRKVMUy9w_TElxVHpZoiixrmQQvHFQSTNLnfufA9-vIj1QFtH5j-5k5OO6kciHH31tXXDk5hjJlJ5ULqPUS?key=HrOhHC0_-ked6RNCpQ0o3PZn)

**IP(Internet protocol):** É o <mark style="background: #ADCCFFA6;">protocolo (Camada de rede) responsável por endereçar e encaminhar os pacotes na rede. Ele não garante que os dados cheguem corretamente ou na ordem certa. Só se preocupa em levar o pacote</mark>.
- Usa endereços IP (ex: 192.168.1.1)
- Pode perder pacotes
- Roteia os pacotes por caminhos diferentes 

**TCP (Transmission Control Protocol):** Protocolo (Camada de transporte) que <mark style="background: #ADCCFFA6;">cuida da confiabilidade da comunicação e garante que os dados cheguem completos, na ordem correta, sem duplicação e sem perda</mark>.  Esse protocolo divide os dados em pacotes numerados, confirma o recebimento e reenvia caso algum pedaço se perca.

**Camadas**
1. **Aplicação:** Onde vivem os protocolos a aplicações que os usuários usam.  É o navegador, o app de e-mail, o YouTube, etc. [1_Arquiteturas da camada de aplicação](../2_Camada%20Aplicação/1_Arquiteturas%20da%20camada%20de%20aplicação.md)
2. **Transporte:** Cuida da entrega dos dados entre dois dispositivos. Responsável pela confiabilidade (TCP) ou velocidade (UDP). [1_Protocolos da camada de transporte da internet](../3_Camada%20de%20Transporte/1_Protocolos%20da%20camada%20de%20transporte%20da%20internet.md)
3. **Rede:** Roteia os pacotes IP até o destino. Escolhe o melhor caminho por onde os dados devem passar.
4. **Enlace:** Transferência de dados entre elementos vizinhos de rede.
5. **Física:** Converte os bits em sinais elétricos, ondas ou luz. Define tensão, frequência, velocidade de bits, etc.

___________________________________________________________________________
### **2. Encapsulamento**

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfXDxDj8GdgLtFqpgESr7V211Ij_eflTjcu7TGmJPmWbHVgKl3nyTo7oGCvHfGQmf9RAsBDhGbJRqwAuKYkPsA4qHkgvenmcHmo6KOLdgcm8wHsx0WU_--fsg_nmyjROetFATgu?key=HrOhHC0_-ked6RNCpQ0o3PZn)

À medida que os dados descem pelas camadas, cada camada adiciona um cabeçalho ao dado original (a mensagem). Isso é chamado de **encapsulamento**.

Na subida (no receptor), os cabeçalhos são removidos um por um, no processo inverso: **desencapsulamento**.

1. **Camada de Aplicação:**
    - **Protocolos:** HTTP, HTTPS, SMTP, FTP, DNS.
    - A Mensagem original (M).
        
2. **Camada de Transporte:**
    - **Protocolos:** TCP ou UDP.
    - **Encapsulamento:** A Camada de Transporte pega a Mensagem (M) e adiciona o cabeçalho de transporte (Ht). A unidade resultante é chamada de **Segmento** (se TCP) ou **Datagrama** (se UDP).
        
    - **Cabeçalho (Ht):** Número da porta de origem e destino, número de sequência (para TCP), etc.
        
    - **Resultado:** `[ Ht | M ]`
        
- **Camada de Rede:**
    
    - **Protocolos:** **IP** (Internet Protocol - IPv4 ou IPv6), ICMP.
        
    - **Encapsulamento:** A Camada de Rede pega o Segmento/Datagrama e adiciona o cabeçalho de rede (Hn). A unidade resultante é chamada de **Pacote** (Packet).
        
    - **Cabeçalho (Hn):** Endereço IP de origem e destino, Tempo de Vida (TTL).
        
    - **Resultado:** `[ Hn | Ht | M ]`
        
- **Camada de Enlace:**
    
    - **Protocolos:** **Ethernet** (para cabos), **Wi-Fi** (IEEE 802.11 - para redes sem fio).
        
    - **Encapsulamento:** A Camada de Enlace pega o Pacote e adiciona o cabeçalho de enlace (Hl) e, geralmente, um trailer/rodapé (T2) para verificação de erros. A unidade resultante é chamada de **Quadro** (Frame).
        
    - **Cabeçalho (Hl):** Endereço físico (MAC) de origem e destino.
        
    - **Trailer (T2):** Detecção de erro (CRC).
        
    - **Resultado:** `[ Hl | Hn | Ht | M | T2 ]`
        
- **Camada Física:**
    
    - **Protocolos:** (Não há protocolos de software aqui, apenas padrões de hardware/sinalização, como 100BASE-TX, 802.11g).
        
    - **Encapsulamento:** Não há cabeçalho. O Quadro é convertido em uma sequência de **Bits** (0s e 1s) para transmissão.
        
    - **Resultado:** Os bits são enviados como sinais elétricos (cabo Ethernet), ondas de rádio (Wi-Fi) ou pulsos de luz (Fibra Óptica).