
---
## **Cliente x Servidor:**

Um ou mais clientes se conectam a um servidor, que é responsável por fornecer serviços ou recursos.

Características:

- Os clientes fazem requisições, e o servidor responde. O servidor não deve iniciar a comunicação com o cliente.
- O servidor tem um ip estático
- O cliente tem um endereço dinâmico. Quando você se conecta à internet, seu roteador ou provedor te dá um IP temporário. Quando você desliga o roteador ou passa um tempo offline, o IP pode ser liberado.
- Clientes não se comunicam diretamente.

---
## **Ponto-a-Ponto (Peer-to-Peer, ou P2P)**

 Cada dispositivo na rede pode agir tanto como cliente quanto como servidor. Ou seja, os usuários compartilham dados entre si diretamente.

Características:

- Não há um servidor central. Se um nó cair, os outros continuam.
- Usa melhor os recursos da rede como um todo.
- Menor custo com infraestrutura central.
- Mais difícil de gerenciar a segurança e o controle.
 
---
## **Híbrida (Cliente-Servidor + P2P)**

 Combina as duas abordagens: existe um servidor para organizar, descobrir ou localizar as conexões, mas a transferência de dados pode ser feita diretamente entre os clientes.

Características:

- O servidor organiza ou autentica os pontos.
- A comunicação entre os peers é direta.
- Combina o melhor dos dois mundos: controle e descentralização.

---
# Exemplos de aplicações p2p e híbridas :
- WhatsApp e Telegram usam servers, mas a mídia vai direto entre usuários.
- Aplicativos de videoconferência (Zoom, Teams): usam servidores pra controle, mas o tráfego pode ser direto entre os participantes.

- O **Napster** permitiu que usuários baixassem músicas diretamente de outros usuários, sem um repositório central. Possua arquitetura Híbrida (P2P + Servidor Central)
	- Servidor Central: Mantinha um índice global de arquivos disponíveis nos PCs dos usuários.
	- Conexão Direta (P2P): Quando um usuário buscava uma música, o servidor listava os peers que tinham o arquivo, e o download ocorria diretamente entre os usuários.
	
- O Gnutella é um protocolo de rede (P2P) criado como uma alternativa descentralizada ao Napster(que dependia de um servidor central). Ele permite que usuários compartilhem arquivos diretamente entre si, sem intermediários.  
	1. Quando um usuário se conecta à rede, ele se torna um nó da rede.	
	2. O usuário pode então enviar uma solicitação de pesquisa para os outros nós da rede. Essa solicitação contém o nome do arquivo que o usuário está procurando. 
	3. Os nós que recebem a solicitação verificam seus próprios arquivos para ver se têm o arquivo procurado. Se tiverem, eles enviam uma resposta ao nó que fez a solicitação, informando a localização. 
	4. Se um nó não tiver o arquivo procurado, ele encaminha a solicitação para outros nós próximos na rede, até que o arquivo seja encontrado ou até que a busca atinja um limite de tempo ou de saltos (**inundação**). 
	O Gnutella pode ser menos eficiente do que outros protocolos P2P mais recentes, pois as solicitações de pesquisa podem percorrer muitos nós antes de encontrar o arquivo desejado.
