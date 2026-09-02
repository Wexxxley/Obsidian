


---

**Spoofing**: refere-se a uma classe de ataques ativos cuja base é a falsificação de identidade em redes de computadores. Consiste em forjar pacotes de dados para que eles pareçam ser originários de uma fonte confiável e previamente autorizada pelo sistema alvo.
- Roubo de dados;
- Acesso não autorizado;
- Redirecionamento malicioso;
- Sabotagem ou espionagem.

---
#### 1. IP Spoofing

O invasor altera o cabeçalho dos pacotes de dados para mascarar o seu verdadeiro endereço IP, substituindo-o pelo IP de uma máquina que possui permissões na rede. 

O  obstáculo para o atacante é o protocolo de comunicação TCP. O TCP exige que as duas máquinas se comuniquem através de uma sequência de números para validar a conexão e checar erros. Para que o IP Spoofing seja bem-sucedido, o invasor não apenas precisa falsificar o IP, mas também interceptar e prever matematicamente essa sequência numérica. 

![350](../../attachments/Pasted%20image%2020260902071418.png)
![400](../../attachments/Pasted%20image%2020260902071940.png)

---
#### 2. Ataque ARP

**ARP** significa Address Resolution Protocol. É um protocolo da camada de rede usado dentro de uma rede local. Em uma rede, cada dispositivo tem dois endereços principais:
    1.  **Endereço IP (Lógico)**: Identifica o dispositivo na rede global.
    2.  **Endereço MAC (Físico)**: Endereço único da placa de rede, gravado em hardware. O virtualBox gera macs lógicos para cada vm.
    
Para que dois dispositivos se comuniquem em uma rede local, eles precisam saber o endereço MAC um do outro. Para isso é enviado um request perguntando o mac:
1. Nenhum dispositivo verifica se a resposta ARP que recebeu veio do dono legítimo do IP.
2. A maioria dos sistemas operacionais atualiza sua tabela ARP com a última resposta que recebeu, sem questionar.

**Man-in-the-Middle (MitM)**: ataque  que explora a vulnerabilidade do ARP.
- O atacante quer se colocar entre a Vítima e o Gateway (o roteador).
- O atacante envia respostas ARP falsificadas para a rede, mentindo sobre o seu próprio endereço MAC.
![450](../../attachments/Pasted%20image%2020260902072544.png)

---
#### 3. DNS Spoofing

O sistema DNS atua como um diretório, traduzindo nomes de domínio legíveis (como o endereço de um site) para endereços IP numéricos que os computadores utilizam para se conectar. O _DNS Spoofing_ consiste em corromper as tabelas de mapeamento deste serviço. Diferente das outras técnicas, esta não exige validações complexas de pacotes. Quando a vítima digita um endereço legítimo no navegador, o servidor DNS manipulado responde com o endereço IP incorreto, pertencente à máquina do atacante. A vítima é então silenciosamente redirecionada para um servidor malicioso que hospeda uma página idêntica à original, criada exclusivamente para a captura e roubo de senhas e dados financeiros (_phishing_).