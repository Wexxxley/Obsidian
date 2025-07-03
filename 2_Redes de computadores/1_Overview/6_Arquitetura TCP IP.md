
Status: #Concluded 

___
# TCP/IP
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfm0yiF7VCzT2a3-JAYru0-quEMlNGUffyxN3fS5Fw5FcE-dLzkcmRKVMUy9w_TElxVHpZoiixrmQQvHFQSTNLnfufA9-vIj1QFtH5j-5k5OO6kciHH31tXXDk5hjJlJ5ULqPUS?key=HrOhHC0_-ked6RNCpQ0o3PZn)

TCP/IP é um conjunto de protocolos de comunicação que permite a troca de dados entre dispositivos em uma rede. Os principais protocolos são o TCP e o IP.

**IP(Internet protocol):** É o protocolo responsável por endereçar e encaminhar os pacotes na rede. Ele não garante que os dados cheguem corretamente ou na ordem certa. Só se preocupa em levar o pacote.
- Usa endereços IP (ex: 192.168.1.1)
- Pode perder pacotes
- Roteia os pacotes por caminhos diferentes 

[1_Protocolos da camada de transporte da internet](../3_Camada%20de%20Transporte/1_Protocolos%20da%20camada%20de%20transporte%20da%20internet.md)
**TCP (Transmission Control Protocol):** Cuida da confiabilidade da comunicação e garante que os dados cheguem completos, na ordem correta, sem duplicação e sem perda.  Esse protocolo divide os dados em pacotes numerados, confirma o recebimento e reenvia caso algum pedaço se perca.

**Camadas**
1. **Aplicação:** Onde vivem os protocolos a aplicações que os usuários usam.  É o navegador, o app de e-mail, o YouTube, etc. [1_Arquiteturas da camada de aplicação](../2_Camada%20Aplicação/1_Arquiteturas%20da%20camada%20de%20aplicação.md)
2. **Transporte:** Cuida da entrega dos dados entre dois dispositivos. Responsável pela confiabilidade (TCP) ou velocidade (UDP). [1_Protocolos da camada de transporte da internet](../3_Camada%20de%20Transporte/1_Protocolos%20da%20camada%20de%20transporte%20da%20internet.md)
3. **Rede:** Roteia os pacotes IP até o destino. Escolhe o melhor caminho por onde os dados devem passar.
4. **Enlace:** Transferência de dados entre elementos vizinhos de rede.
5. **Física:** Converte os bits em sinais elétricos, ondas ou luz. Define tensão, frequência, velocidade de bits, etc.

___________________________________________________________________________
# Encapsulamento

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfXDxDj8GdgLtFqpgESr7V211Ij_eflTjcu7TGmJPmWbHVgKl3nyTo7oGCvHfGQmf9RAsBDhGbJRqwAuKYkPsA4qHkgvenmcHmo6KOLdgcm8wHsx0WU_--fsg_nmyjROetFATgu?key=HrOhHC0_-ked6RNCpQ0o3PZn)

À medida que os dados descem pelas camadas, cada camada adiciona um cabeçalho ao dado original (a mensagem). Isso é chamado de **encapsulamento**.

Na subida (no receptor), os cabeçalhos são removidos um por um, no processo inverso: **desencapsulamento**.

1. **Camada de Aplicação:** Mensagem M. Não adiciona cabeçalho específico no modelo, mas o protocolo da aplicação (ex: HTTP, SMTP) define um formato.
2. **Camada de Transporte**: Ht: Número de porta de origem e destino, número de sequência e etc.
3. **Camada de Rede:** Hn: Endereço IP de origem e destino, Tempo de vida (TTL).
4. **Camada de Enlace:** Hl: Endereço físico (MAC) de origem e destino. Tipo do protocolo da camada superior (ex: IP), Detecção de erro (CRC)
5. **Camada Física:** Não há cabeçalho real, os dados são apenas convertidos em sinais elétricos, ópticos ou de rádio.