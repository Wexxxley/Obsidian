
#Concluded 

---
### **1. Three-tier architecture**

Esse é o fluxo mais básico de System Design. A arquitetura de três camadas é um modelo de software que divide uma aplicação em três camadas independentes:
- **Apresentação:** O que você vê e toca na tela. Páginas web no seu navegador.
- **Lógica de Negócios:** Onde as regras acontecem.
- **Dados:** Onde ficam guardadas as informações de usuários, produtos e senhas de forma segura.

**Vantagens**
- **Organização:** Cada parte funciona sozinha, então mudar o visual não estraga o banco de dados.
- **Crescimento:** Permite escalar as camadas de formas diferentes de acordo com a necessidade.

![](../../attachments/Pasted%20image%2020260804091025.png)
**Requisições Síncronas**: Ocorre quando o cliente envia uma solicitação ao servidor e bloqueia a sua execução, aguardando a resposta. A conexão de rede permanece aberta e o processo aguarda até que o servidor conclua o processamento e retorne um código de status.

**Requisições Assíncronas**: Permite que o sistema envie uma solicitação e continue executando outras operações sem ficar travado.
- **WebSockets:** O WhatsApp Web utiliza majoritariamente o protocolo WebSocket. Diferente do protocolo HTTP padrão (onde o cliente precisa iniciar cada requisição), o WebSocket estabelece uma conexão persistente e bidirecional. Devido a essa conexão, o servidor possui a capacidade enviar mensagens para o cliente diretamente.

**Requisições "Fire-and-Forget"**: Utilizado quando o emissor da requisição não necessita da resposta para dar continuidade ao seu fluxo de trabalho.
- **Comunicação Servidor-Servidor:** O Servidor A envia a informação para o Servidor B e encerra a comunicação, considerando a tarefa concluída. O Servidor B processa no seu tempo.

---
### 2. Escalonamento

**Horizontal**: É a duplicação de servidores, múltiplas instâncias de servidores trabalhando em paralelo. Um componente chamado **balanceador de carga/Load Balancer** recebe o tráfego de rede e o distribui entre as instâncias.
- **Arquitetura Stateful:** Se o Servidor 1 armazenar dados localmente teremos problema de compartilhamento de dados entre os servidores.
- **Arquitetura Stateless:** Nenhum dado necessário para o funcionamento da aplicação pode ser gravado localmente no servidor. O armazenamento deve ser isolado em sistemas externos centralizados, como bancos de dados.
![600](../../attachments/Pasted%20image%2020260804092616.png)

**Vertical**: A ampliação ocorre por meio do incremento de recursos físicos. Isso inclui a alocação de mais núcleos de CPU, expansão da RAM e utilização de discos de armazenamento mais velozes.
- **Limitação de Hardware:** Há uma capacidade máxima de recursos que uma placa-mãe ou instância em nuvem consegue suportar. 
- **Disponibilidade e Falhas:** A alteração das especificações do servidor exige, na maioria dos casos, o desligamento e a reinicialização do sistema, resultando em tempo de inatividade. Além disso, concentrar toda a operação em uma máquina cria um ponto único de falha.

---
### **3. Princípio Stateless** 

Na arquitetura cliente-servidor original, especialmente sob as restrições do protocolo HTTP e do estilo arquitetural REST, o sistema deve ser stateless. Isso significa que o servidor não deve armazenar nenhum contexto ou histórico sobre as requisições anteriores localmente.
- **Autossuficiência das Requisições:** Cada solicitação deve conter absolutamente todas as informações necessárias para que o servidor consiga processá-la de forma isolada. 
- **Gestão de Estado no Cliente:** A responsabilidade de manter e gerenciar o estado da sessão é transferida para o cliente. O cliente reenvia esse estado ao servidor a cada nova interação.

O princípio stateless é o principal viabilizador do crescimento de sistemas.
- **Escalonamento Horizontal Facilitado:** Como nenhuma máquina armazena sessões locais, o tráfego pode ser distribuído homogeneamente por um balanceador de carga. Qualquer servidor instanciado  é capaz de processar qualquer requisição recebida.
- **Tolerância a Falhas:** Se um servidor apresentar defeito, o usuário não perde o seu acesso. A próxima requisição simplesmente será roteada para outro servidor.
- **Sobrecarga de Rede:** Como o servidor não lembra quem é o usuário, o cliente é obrigado a anexar o seu contexto repetidamente no cabeçalho de todas as requisições, gerando um tráfego de dados constante e repetitivo (**overhead de rede**).