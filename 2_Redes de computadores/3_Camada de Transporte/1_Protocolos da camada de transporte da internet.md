
---

  Se a camada de rede leva dados de máquina para máquina. A camada de transporte leva dados de programa para programa. É a parte responsável por oferecer comunicação entre processos que estão sendo executados em diferentes dispositivos. Ela garante que os dados de uma aplicação cheguem corretamente no destino, cuidando de controle de erros, controle de fluxo e controle de congestionamento.

---
# TCP (Transmission control protocol): 
- **Transmissão confiável**: garante que todos os pacotes cheguem. É feito o reenvio caso necessário.
- **Orientado à conexão:** antes de enviar, ele estabelece uma conexão com o outro lado.
- **Controle de fluxo**: o transmissor não sobrecarrega o receptor, o transmissor envia em uma taxa que seja suportada pelo receptor.
- **Controle de congestionamento:** protege a rede do excesso de tráfego, envia em uma taxa que seja suportada pela rede.
- O TCP não garante **temporização**, ou seja,  que os dados chegarão em um tempo específico. Pode demorar 1, 10 segundos.

---
# UDP (User Datagram Protocol): 
- Não oferece estabelecimento de conexão. Os pacotes são enviados sem garantir que o destino esteja pronto para recebê-los.
- Mais rápido, pois não tem controle de erros nem verificação
- Não garante que os dados cheguem ao destino, nem que cheguem corretamente ou na ordem certa. Se um pacote for perdido ou corrompido, ele não será retransmitido.
- A UDP não garante nada, apenas velocidade. Sendo assim a aplicação pode criar algum tipo de protocolo que garanta um pouco mais a integridade das informações.  

**Checksum**: O checksum do UDP é uma técnica usada para garantir a integridade dos dados, ajudando a verificar se o conteúdo do pacote chegou intacto ao destino. 

O checksum é calculado pelo remetente antes do envio e verificado pelo receptor ao receber o pacote. Se o valor do checksum recebido não corresponde, significa que houve algum erro durante a transmissão. Sendo assim, o receptor sabe que algo deu errado e pode, por exemplo, ignorar o pacote.

---
**Filosofia do TCP:** "Precisamos garantir que tudo chegue perfeitamente, mesmo que seja mais lento." 
	-Ideias para aplicações que não toleram erros, como o download de um arquivo

**Filosofia do UDP:** "Precisamos que os dados cheguem o mais rápido possível, mesmo que alguns se percam."
- Ideia para aplicações em tempo real que precisam de alta velocidade, como streaming.
