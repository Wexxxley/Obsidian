

---
As redes no Docker são uma abstração criada para facilitar a comunicação entre contêineres, entre contêineres e o host, e até entre contêineres em hosts diferentes. O Docker vem com três redes padrão: bridge, host e none. 

### **1. Default Bridge**

Por padrão, quando você não especifica nada, o Docker realiza uma "mágica" para que tudo funcione, mas é importante entender o que acontece nos bastidores.

- **A Interface docker0**: Ao instalar o Docker, ele cria uma interface de rede virtual no seu host chamada `docker0`. Essa é a "default bridge".
    
- Quando você inicia um container, o Docker cria interfaces virtuais que conectam esse container à ponte `docker0`. É como se fosse um switch virtual.
    
- **NAT e Isolamento**: Os containers ganham seus próprios endereços IP internos. Eles conseguem acessar a internet através do host usando NAT (Network Address Translation), mas o mundo externo (incluindo você no seu navegador) não consegue acessar o container diretamente pelo IP dele por padrão.
    
- **Expondo Portas**: Para acessar um serviço rodando no container, você precisa fazer o mapeamento de portas manualmente (ex: `docker run -p 80:80`). Isso diz ao Docker para pegar o tráfego da porta 80 do seu host e enviar para a porta 80 do container.

---
### **2. Pontes Definidas pelo Usuário**

Embora a Default Bridge funcione, a recomendação oficial do Docker é que você crie suas próprias redes. 

**Criando a Rede:** 
- `docker network create <nome-da-rede>`

**Conectando Containers:** Ao criar um container, você usa a flag --network para colocá-lo nessa nova rede:
- `docker run --network <nome-da-rede> ...`    

**Vantagem 1: DNS Mágico (Service Discovery)**: Na Default Bridge, os containers só conseguem se comunicar sabendo o endereço IP um do outro (que muda sempre). Na User-Defined Bridge, o Docker habilita um DNS automático. Isso facilita muito a comunicação entre serviços (ex: um container de aplicação web falando com um banco de dados pelo nome).

**Vantagem 2: Isolamento**: Containers em uma rede criada por você (ex: "asgard") estão isolados da rede padrão e de outras redes personalizadas. Isso é crucial para segurança, impedindo que containers não relacionados conversem entre si.
