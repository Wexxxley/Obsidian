
---

Motivações:
- O espaço de endereços de 32 bits estaria próximo de ser completamente alocado entre 2008 e 2018.
- Melhorar o formato do cabeçalho para permitir maior velocidade de processamento e de transmissão.
- Mudanças no cabeçalho para incorporar mecanismos de controle de QoS.

As mudanças mais importantes introduzidas no IPv6 foram: 
- **Capacidade de endereçamento expandida**. O IPv6 aumenta o tamanho do endereço IP de 32 bits para 128 bits. Isso garante que o mundo não ficará sem endereços IP.
- **Cabeçalho aprimorado de 40 bytes.** Vários campos IPv4 foram descartados ou tornaram-se opcionais. O cabeçalho de comprimento fixo de 40 bytes resultante permite processamento mais veloz do datagrama IP.
- **Rotulação de fluxo e prioridade**. O RFC 1752 e o RFC 2460 declaram que isso permite “rotular pacotes que pertencem a fluxos particulares para os quais o remetente requisita tratamento especial, tal como um serviço de qualidade não padrão ou um serviço de tempo real”. Por exemplo, a transmissão de áudio e vídeo seria tratada como um fluxo. Por outro lado, aplicações mais tradicionais, como transferência de arquivos e e-mail, poderiam não ser tratadas assim. É possível que o tráfego carregado por um usuário de alta prioridade (digamos, alguém que paga por um serviço melhor de tráfego) seja também tratado como um fluxo. O que fica claro, contudo, é que os projetistas do IPv6 preveem a possível necessidade de conseguir diferenciá-los, mesmo que o exato significado de fluxo ainda não tenha sido determinado. O cabeçalho IPv6 também tem um


Cabeçalho fixo de 40 bytes. Não é permitida fragmentação nos roteadores
(apenas fonte
![[Pasted image 20250530105010.png]]