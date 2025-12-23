
#Concluded 

---
 Se a camada de rede leva dados de máquina para máquina. <mark style="background: #ADCCFFA6;">A camada de transporte leva dados de programa para programa</mark>. É a parte responsável por oferecer comunicação entre processos que estão sendo executados em diferentes dispositivos. 

### **1. TCP (Transmission control protocol)**

- **Transmissão confiável**: garante que todos os pacotes cheguem. Reenvia caso necessário.
- **Orientado à conexão:** antes de enviar, ele estabelece uma conexão com o outro lado.
- **Controle de fluxo**: o transmissor não sobrecarrega o receptor, o transmissor envia em uma taxa que seja suportada pelo receptor.
- **Controle de congestionamento:** protege a rede do excesso de tráfego, envia em uma taxa que seja suportada pela rede.
- O TCP não garante **temporização**, ou seja,  que os dados chegarão em um tempo específico. Pode demorar 1, 10 segundos.
- ==Ideias para aplicações que não toleram erros, como o download de um arquivo==

### **2. UDP (User Datagram Protocol)**

- **Não possui transimissao confiável.** Não garante que os dados cheguem ao destino, nem que cheguem corretamente ou na ordem certa.
- **Não oferece estabelecimento de conexão**. Os pacotes são enviados sem garantir que o destino esteja pronto para recebê-los.
- Mais rápido, pois **não tem controle de erros nem verificação**
- A UDP não garante nada, apenas velocidade. Sendo assim a aplicação pode criar algum tipo de protocolo que garanta um pouco mais a integridade das informações.  
-  ==Ideia para aplicações em tempo real que precisam de alta velocidade, como streaming.==

**Checksum**: O checksum do UDP é uma técnica usada para garantir a integridade dos dados, ajudando a verificar se o conteúdo do pacote chegou intacto ao destino. O checksum é calculado pelo remetente antes do envio e verificado pelo receptor ao receber o pacote. Se o valor do checksum recebido não corresponde, significa que houve algum erro durante a transmissão. 