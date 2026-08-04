

---
### **1. Three-tier architecture**

Esse é o fluxo mais básico de System Design. A arquitetura de três camadas é um modelo de software que divide uma aplicação em três camadas independentes:
- **Apresentação:** O que você vê e toca na tela. Páginas web no seu navegador.
- **Lógica de Negócios:** Onde as regras acontecem, calculando preços, validando senhas e decidindo o que fazer com os dados.
- **Dados:** Onde ficam guardadas as informações de usuários, produtos e senhas de forma segura.

**Vantagens**
- **Organização:** Cada parte funciona sozinha, então mudar o visual não estraga o banco de dados.
- **Crescimento:** Permite escalar as camadas de formas diferentes de acordo com a necessidade.

![](../../attachments/Pasted%20image%2020260804091025.png)
**Requisições Síncronas**: Uma requisição síncrona ocorre quando o cliente envia uma solicitação ao servidor e bloqueia a sua execução, aguardando a resposta para poder prosseguir. A conexão de rede permanece aberta e o processo aguarda até que o servidor conclua o processamento e retorne um código de status.

**Requisições Assíncronas**: Uma requisição assíncrona permite que o sistema envie uma solicitação e continue executando outras operações sem ficar travado.
- **WebSockets:** O WhatsApp Web utiliza majoritariamente o protocolo WebSocket. Diferente do protocolo HTTP padrão (onde o cliente precisa iniciar cada requisição), o WebSocket estabelece uma conexão persistente e bidirecional entre o navegador e o servidor. Devido a essa conexão contínua, o servidor possui a capacidade de empurrar mensagens para o cliente, eliminando a necessidade de o cliente fazer requisições constantes.

**Requisições "Fire-and-Forget"**: Utilizado quando o emissor da requisição não necessita da resposta para dar continuidade ao seu fluxo de trabalho.
- **Comunicação Servidor-Servidor:** O Servidor A envia a informação para o Servidor B e encerra o seu processo de comunicação, considerando a tarefa concluída. O Servidor B recebe o dado e realiza a gravação no banco de dados em seu próprio tempo.
### 2. Escalonamento

**Horizontal**: É a duplicação de servidores, múltiplas instâncias de servidores trabalhando em paralelo. Um componente chamado **balanceador de carga/Load Balancer** recebe o tráfego de rede e o distribui entre as instâncias.

- **Arquitetura Stateful:** Se o Servidor 1 armazenar dados localmente teremos problema de compartilhamento de dados entre os servidores
- **Arquitetura Stateless:** Nenhum dado necessário para o funcionamento da aplicação pode ser gravado localmente no servidor. O armazenamento deve ser isolado em sistemas externos centralizados, como bancos de dados externos, sistemas de armazenamento em nuvem e caches distribuídos em memória (Redis).


O escalonamento vertical consiste em aumentar a capacidade computacional de um servidor já existente, em vez de adicionar novas instâncias à infraestrutura.

- **Funcionamento:** A ampliação ocorre por meio do incremento de recursos físicos ou virtuais da mesma máquina. Isso inclui a alocação de mais núcleos de processamento (CPU), expansão da memória RAM e utilização de discos de armazenamento mais velozes ou com maior capacidade.
    
- **Arquitetura e Estado:** A infraestrutura mantém um desenho simples, sem a necessidade de balanceadores de carga (_Load Balancers_), pois todo o tráfego de rede continua sendo direcionado para o mesmo ponto. Devido a isso, o armazenamento local de dados (arquitetura _stateful_) não gera inconsistências. Todas as requisições acessarão a mesma memória e o mesmo disco, encontrando as sessões e arquivos gravados.
    
- **Limitação de Hardware:** A principal desvantagem deste modelo é a existência de um limite físico. Há uma capacidade máxima de recursos que uma placa-mãe ou instância em nuvem consegue suportar. Quando o hardware atinge a especificação máxima disponível no mercado ou no provedor, o sistema não pode mais crescer dessa maneira.
    
- **Disponibilidade e Falhas:** A alteração das especificações do servidor exige, na maioria dos casos, o desligamento e a reinicialização do sistema, resultando em tempo de inatividade (_downtime_). Além disso, concentrar toda a operação em uma máquina cria um ponto único de falha (_Single Point of Failure_). Caso ocorra um defeito físico no hardware, a aplicação inteira fica fora do ar até o reparo.