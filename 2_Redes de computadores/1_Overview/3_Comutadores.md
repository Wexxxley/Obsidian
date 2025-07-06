Status: #Concluded 

---
# 1. Comutadores
**Sistemas finais** são conectados entre si por **enlaces de comunicação** e **comutadores de pacotes.** Quando um sistema final possui dados para enviar a outro, o sistema emissor segmenta esses dados e adiciona bytes de cabeçalho a cada segmento. Os pacotes resultantes, conhecidos como pacotes/datagrama são enviados ao sistema final de destino, onde são remontados para os dados originais. 

 Um comutador de pacotes é um ==dispositivo responsável por encaminhar pacotes de dados em uma rede.== Ele recebe um pacote e decide para qual enlace de saída ele deve enviá-lo, com base nas informações do pacote e nas regras da rede. Existem dois principais tipos de comutadores:

1. **Roteadores:**  Faz o encaminhamento de pacotes entre redes de computadores distintas, baseados em endereços IP.     
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcvHvHRxM-n17unge1tgm-6hfOQWwMIkzkllRcbUnykpkdeRaDCLmgzeyvRPl6psinEjBad8GRM3naY6IFqUcvNMRTPShVov_Hzzx96M8eLey9ubNpa7oKOxv7mbRCYxLPJnykahg?key=HrOhHC0_-ked6RNCpQ0o3PZn)

2. **Switches:** São utilizados em redes de acesso, ou seja, em redes locais (LANs), como em empresas e residências. Eles operam em um nível mais baixo da comunicação e conectam dispositivos dentro de uma mesma rede. Ele possui várias portas para conexão e armazena os endereços MAC (identificação única de cada dispositivo na rede) em uma tabela.  
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdv1znrP314K2Hrm9SA9MY66nvlKa6hBkpiuEigO-zbZG2PLW-VDyuVs6HZU9YGPScE0LSKv_tcAltwjHyyVhNlkrw78jCy1wig2myvlgAfnNzdp6J8JS4D6n2FWkY2LkVURlF7vA?key=HrOhHC0_-ked6RNCpQ0o3PZn)
 

 A **rota** é a sequência de enlaces e comutadores que um pacote percorre desde o remetente até o destinatário.

**Protocolos de rede**
“Um protocolo define o formato e a ordem das mensagens trocadas entre duas ou mais entidades comunicantes, bem como as ações realizadas na transmissão e/ou no recebimento de uma mensagem ou outro evento.”