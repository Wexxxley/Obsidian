


---

Spoofing ataque ativo onde o sujeito autentica um host para outro se utilizando da técnica de forjar pacotes originários de um host confiável. ⚫ Objetivos: ⚫ Roubo de dados ⚫ Acesso não autorizado ⚫ Redirecionamento malicioso ⚫ Sabotagem ou espionagem ⚫ Os principais e mais largamente utilizados tipos de spoofing são: ⚫ IP Spoofing; ⚫ ARP Spoofing; ⚫ DNS Spoofing

### 1. Ataque ARP

**ARP** significa Address Resolution Protocol. É um protocolo da camada de rede usado dentro de uma rede local. Em uma rede, cada dispositivo tem dois endereços principais:
    1.  **Endereço IP (Lógico)**: Identifica o dispositivo na rede global.
    2.  **Endereço MAC (Físico)**: Endereço único da placa de rede, gravado em hardware. O virtualBox geras macs lógicos para cada vm.
    
Para que dois dispositivos se comuniquem em uma rede local, eles precisam saber o endereço MAC um do outro. Para isso é enviado um request perguntando o mac:
1.  Nenhum dispositivo verifica se a resposta ARP que recebeu veio do dono legítimo do IP.
2.  A maioria dos sistemas operacionais atualiza sua tabela ARP com a última resposta que recebeu, sem questionar.

**Man-in-the-Middle (MitM)**: ataque  que explora a vulnerabilidade do ARP.
- O atacante quer se colocar entre a Vítima e o Gateway (o roteador).
- O atacante envia respostas ARP falsificadas para a rede, mentindo sobre o seu próprio endereço MAC.
