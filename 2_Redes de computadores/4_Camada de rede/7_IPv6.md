#Concluded 

---

Motivações:

- O espaço de endereços de 32 bits é relativamente pouco.
- Melhorar o cabeçalho para permitir maior velocidade de processamento e de transmissão.
- Mudanças no cabeçalho para incorporar controle de **Qualidade de serviço(QoS).**

As mudanças mais importantes introduzidas no IPv6 foram: 

- **Capacidade de endereçamento expandida**. O IPv6 aumenta o tamanho do endereço IP de 32 bits para 128 bits. Isso garante que o mundo não ficará sem endereços IP.
- **Cabeçalho aprimorado de 40 bytes.** Vários campos IPv4 foram descartados. O cabeçalho de comprimento fixo de 40 bytes resultante permite processamento mais veloz do datagrama IP.
- **Rotulação de Fluxo:** O IPv6 introduz um campo chamado "Rótulo de Fluxo" para identificar pacotes que pertencem a um mesmo "fluxo". Um "fluxo" é uma sequência de pacotes que o remetente deseja que recebam tratamento especial, como garantia de qualidade de serviço (QoS) ou transmissão em tempo real (ex: áudio e vídeo).
- **Prioridade (Classe de Tráfego):** O cabeçalho IPv6 também possui um campo de 8 bits para "Classe de Tráfego" (Traffic Class). Este campo permite que os datagramas sejam priorizados.
![Pasted image 20250530105010](../../attachments/Pasted%20image%2020250530105010.png)
- **Versão**. Esse campo de 4 bits identifica o número da versão do IP. 
- **Classe de tráfego.** Identifica o a classe dos dados para poder dar prioridade.
- **Rótulo de fluxo**. Esse campo de 20 bits é usado para identificar um fluxo de datagramas. 
- **Comprimento da carga útil.** 
- **Próximo cabeçalho**. Esse campo identifica o protocolo ao qual o conteúdo desse datagrama será entregue (por exemplo, TCP ou UDP). 
- **Limite de saltos.** 
- **Endereços de origem e de destino.** 
- **Dados**. Carga útil do datagrama IP.
 
 **Fragmentação/remontagem:** O IPv6 não permite fragmentação e remontagem. Se um datagrama IPv6 recebido por um roteador for muito grande para ser repassado pelo enlace de saída, o roteador apenas descartará o datagrama e devolverá ao remetente uma mensagem de erro ICMP “Pacote muito grande”. O remetente pode então reenviar os dados usando um datagrama IP de tamanho menor.  Fragmentação e remontagem são operações que tomam muito tempo; retirar essas funcionalidades dos roteadores e colocá-las nos sistemas finais acelera consideravelmente o repasse IP para dentro da rede. 

**ICMPv6**: nova versão do ICMP
- Tipos de mensagens adicionais , ex.: “Packet Too Big”.
