


---
### 1. Tipos de hackers

**Hackers Éticos (White Hat):** Profissionais especializados que atuam com o objetivo de identificar e corrigir vulnerabilidades em sistemas operacionais e redes que já estão em funcionamento.
- Se adotam posturas mais agressivas em suas ações, podem ser classificados também sob a nomenclatura de **Red Hat Hackers.**
    
**Hackers Maliciosos (Black Hat):** As suas motivações primárias incluem a obtenção de acesso não autorizado a sistemas privados, o roubo de informações confidenciais ou a intenção deliberada de causar danos estruturais e financeiros. 
      
**Hackers Cinzas (Grey Hat):** Caracterizam-se por operar em uma zona intermediária entre os extremos éticos e maliciosos. A sua motivação central é identificar e alertar as organizações sobre as vulnerabilidades existentes em suas redes, contudo, realizam essas atividades investigativas sem possuírem a permissão prévia ou explícita dos proprietários dos sistemas. 
    
**Hacktivistas:** São hackers que direcionam os seus conhecimentos para a promoção e defesa de causas políticas ou sociais. A motivação fundamental desse grupo é realizar declarações públicas de impacto. Não atuam conforme a lei.
- WikiLeaks: Organização transnacional que atua no vazamento de dados governamentais e corporativos. A sua motivação é promover a transparência radical.
    
**Blue Hat Hackers:** Hackers contratados para testar sistemas antes de serem lançados.
    
**Green Hat Hackers:** Novatos e aprendizes no campo da segurança cibernética que encontram-se nas fases iniciais de estudo sobre as técnicas e conceitos de hacking.

**Script Kiddies:** indivíduos que possuem habilidades limitadas, dependendo de forma integral da utilização de softwares e ferramentas maliciosas.

---
### 2. Classificação do ataques

1. De acordo com o impacto sobre os ativos ou recursos;
2. De acordo com a finalidade da ação maliciosa.
#### 2.1 De acordo com o impacto sobre os ativos ou recursos

- **Ataques Passivos:** Possuem a natureza de bisbilhotar ou monitorar as transmissões.
	- Tenta descobrir ou utilizar informações do sistema sem afetar os recursos.
	- Difíceis de detectar (prevenção ao invés de detecção)
    ![400](../../attachments/Pasted%20image%2020260901152833.png)
- **Ataques Ativos:** Tentam alterar os recursos de um sistema ou afetar a sua operação. Modificam o fluxo de dados ou criam um fluxo falso.
	![400](../../attachments/Pasted%20image%2020260901152711.png)
    ![400](../../attachments/Pasted%20image%2020260901152805.png)

#### 2.2 Ataques por Finalidade

- **Recuperação de Informações:** Englobam técnicas cujo objetivo é a coleta de dados do sistema ou dos usuários. 
	- **Packet Sniffing:** captura de pacotes de dados que trafegam em uma rede. O **wireshark** é um sniffer.
	- **Engenharia Social:** uso da persuasão, explorando a ingenuidade ou a confiança do usuário, para obter informações que podem ser utilizadas para ter acesso não autorizado a computadores ou informações.
		- **Phishing:**  se dá através do envio de mensagem não solicitada, passando-se por comunicação de uma instituição conhecida, como um banco, empresa ou site popular, e que procura induzir o acesso a páginas  falsificadas, projetadas para furtar dados. O  golpe do WhatsApp tbm se enquadra.
	- **Port Scanning:** Varredura automatizada nas portas de comunicação de um servidor para identificar quais estão abertas e mapear possíveis pontos de entrada. 
		- Descoberta de hosts, Detecção de versão, Detecção do sistema operacional, etc.
	- **Scanning de Vulnerabilidades:** Técnica  que varre sistemas e redes em busca de falhas de segurança conhecidas e configurações enfraquecidas.
		- Ocorre após o Port Scanning. 
	
- **Falsificação:** A falsificação de identidade é operada através de técnicas de Spoofing, que permitem a um atacante assumir a identidade de um remetente legítimo.

- **Negação de serviço:** Visam comprometer a disponibilidade dos recursos.
    
- **Códigos Maliciosos (Malware):** 
	- **Vírus:** Programa que se anexa a outros arquivos e necessita da ação do usuário para se executar e infectar o sistema.
	- **Cavalos de Troia (Trojans):** Malware que se disfarça de um programa legítimo e inofensivo para enganar o usuário e abrir portas para outras ameaças.
	- **Adware:** Software projetado para exibir anúncios indesejados e intrusivos na tela do dispositivo do usuário.
	- **Spyware:** Programa espião que monitora secretamente as atividades do usuário e coleta seus dados para enviá-los a terceiros.
	- **Keyloggers:** Tipo de spyware que registra de forma oculta todas as teclas digitadas pelo usuário no teclado.
	- **Screenloggers:** Variação de spyware que captura imagens da tela do dispositivo em momentos específicos, como ao clicar com o mouse.
	- **Backdoors:** Mecanismo inserido em um sistema para garantir um acesso remoto oculto e contínuo ao invasor, ignorando a autenticação padrão.
	- **Worms:** Código autorreplicável que se propaga pelas redes explorando vulnerabilidades, sem precisar de interação humana.
	- **Bots:** Programas que infectam um computador e permitem que ele seja controlado remotamente por um atacante para realizar tarefas automatizadas.
	- **Botnets:** Rede de múltiplos computadores infectados controlados por um atacante para realizar ações coordenadas, como ataques de negação de serviço.