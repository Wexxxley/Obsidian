
State: #Concluded 

___
# 1 Correio eletrônico e SMTP

Os componentes são:
1. **Agentes de Usuário**: são apps que permitem aos usuários ler, compor e enviar e-mails. Eles funcionam como a interface entre o usuário e o sistema de e-mail. Como, Eudora, Outlook. Esses apps se conectam a servidores de correio para enviar e receber mensagens.
2. **Servidores de Correio:** Esses servidores são configurados para enviar, armazenar e entregar as mensagens. O agente do usuário é o cliente, ele envia um email e o servidor de correio recebe e repassa. Em caso de falha, ele fica tentando enviar a cada 30 minutos durante 5 dias.
3. **SMTP - Simple Mail Transfer Protocol**: O SMTP é o protocolo usado para enviar e-mails entre servidores de correio. O SMTP usa o protocolo de transferência TCP pela confiabilidade.

![Pasted image 20250508163157](../../attachments/Pasted%20image%2020250508163157.png)

**Sem autenticação**
 O SMTP é muito antigo, foi criado nos anos 80. Naquela época, a internet era usada por poucos e não havia preocupação com segurança. Por isso, o SMTP não tem autenticação embutida.  O SMTP só entrega a mensagem, ele não valida o remetente. É por isso que é fácil falsificar o campo From: em um e-mail, e isso é a base de phishing e spam.

**Base 64**
 O SMTP foi feito para transmitir apenas texto ASCII, ou seja, só letras básicas do inglês e símbolos simples, além disso, pela limitação da época os dados binários eram codificados em 6 bits.

 Com o passar do tempo, foi necessário lidar com o envio de arquivos multimídia. A solução improvisada foi codificar arquivos em Base64. A Base64 transforma dado binário (imagem, áudio, PDF) em texto ASCII, para poder passar pelo SMTP. Isso é ineficiente, a codificação Base64 aumenta o tamanho do arquivo, é mais lenta e consome mais banda.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXewaT_qePpqMoVaf6vqhOVRCzf2d3PUYVOgIvLz7oKnDMV6rSwt8mDnvQ2myeVwQPmu0WvbFXJoVwDhOdWwBhQkd1w_cPHbgOKcSND-pEXymqGKo6Y537QoCGO2xVSXBKC6Cg6aoQ?key=HrOhHC0_-ked6RNCpQ0o3PZn)

**Cenário de envio**
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfm8utei6yDoNeXLzDA12hupmUBBnyJTQd0dGQjgxEfGAzxG-yICVSBXC0nKzP7b8MoC-SHb-0NbddaVD3hkSJNGeNDkOVNQjIWdvoSX26UtuX57t1sr_3oqcNoO2uGb18H4FYOOQ?key=HrOhHC0_-ked6RNCpQ0o3PZn)
1) Alice usa o agente de usuário para compor a msg.
2) O agente envia a msg para o seu servidor de correio que é colocada na fila.
3) O lado cliente SMTP abre uma conexão TCP DIRETA com o servidor do Bob.
4) O cliente SMTP envia a msg de Alice pela conexão TCP.
5) O servidor de correio de Bob coloca a msg na caixa de correio de Bob.
6) Bob invoca seu agente de usuário para ler a msg.
---
# 2.Protocolos de acesso
Protocolos de acesso são usados para recuperar e-mails do servidor para o agente de usuário.

**POP3 (Post Office Protocol v3):** Protocolo extremamente simples e stateless, não permite criação de pastas no servidor, recomendado para quem acessa e-mails por um único dispositivo. Ele possui 3 fases:
- Autorização (login e senha)
- Transação (baixar mensagens, marcar para deletar, ver estatísticas)
- Atualização (AO SAIR, é feita as atualizações)

**IMAP (Internet Mail Access Protocol):** Mais completo que o POP3. Ele permite ==criar e gerenciar pastas no servidor==, ==sincronização em tempo real entre dispositivos== e mantém estado entre seções.

**HTTP para Webmail:**  Gmail, Outlook, etc. usam HTTP/HTTPS para acessar e-mails via navegador.A comunicação entre os servidores ainda é feita por SMTP.

