
#Concluded 

___
### **1. Arquitetura TCP/IP**

Modelo abstrato que define como os componentes da rede se organizam e interagem para permitir a comunicação entre dispositivos. Essa arquitetura define um conjunto de protocolos de comunicação.
![500](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfm0yiF7VCzT2a3-JAYru0-quEMlNGUffyxN3fS5Fw5FcE-dLzkcmRKVMUy9w_TElxVHpZoiixrmQQvHFQSTNLnfufA9-vIj1QFtH5j-5k5OO6kciHH31tXXDk5hjJlJ5ULqPUS?key=HrOhHC0_-ked6RNCpQ0o3PZn)

1. **Aplicação:** Onde vivem os protocolos da aplicações que os usuários usam.  É o navegador, o app de e-mail, o YouTube, etc. 
2. **Transporte:** Cuida da entrega dos dados entre dois dispositivos. Responsável pela confiabilidade (TCP) ou velocidade (UDP). [1_Protocolos da camada de transporte da internet](../3_Camada%20de%20Transporte/1_Protocolos%20da%20camada%20de%20transporte%20da%20internet.md)
3. **Rede:** Roteia os pacotes IP até o destino. Escolhe o melhor caminho por onde os dados devem passar.
4. **Enlace:** Transferência de dados entre elementos vizinhos de rede.
5. **Física:** Converte os bits em sinais elétricos, ondas ou luz. Define tensão, frequência, velocidade de bits, etc.


**IP(Internet protocol):** É o <mark style="background: #ADCCFFA6;">protocolo (Camada de rede) responsável por endereçar e encaminhar os pacotes na rede. Ele não garante que os dados cheguem corretamente ou na ordem certa. Só se preocupa em levar o pacote</mark>.

**TCP (Transmission Control Protocol):** Protocolo (Camada de transporte) que <mark style="background: #ADCCFFA6;">cuida da confiabilidade da comunicação e garante que os dados cheguem completos, na ordem correta, sem duplicação e sem perda</mark>.  


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
    - **Encapsulamento:** A Camada de Transporte pega a Mensagem (M) e adiciona o cabeçalho de transporte (Ht). A unidade resultante é chamada de **Segmento**.
        
3. **Camada de Rede:**
    - **Protocolos:** IP (Pv4 ou IPv6)
    - **Encapsulamento:** A Camada de Rede pega o Segmento/Datagrama e adiciona o cabeçalho de rede. A unidade resultante é chamada de **Pacote**.
        
4. **Camada de Enlace:**
    - **Protocolos:** Ethernet (para cabos), Wi-Fi (para redes sem fio).
    - **Encapsulamento:** A Camada de Enlace pega o Pacote e adiciona o cabeçalho de enlace (Hl). A unidade resultante é chamada de **Quadro**.
        
5. **Camada Física:**
    - **Protocolos:** (Não há protocolos de software aqui, apenas padrões de hardware).
    - **Encapsulamento:** Não há cabeçalho. O Quadro é convertido em uma sequência de bits.
