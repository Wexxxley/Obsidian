

---
As redes no Docker são uma abstração criada para facilitar a comunicação entre contêineres, entre contêineres e o host, e até entre contêineres em hosts diferentes. 

O Docker vem com três redes padrão: **bridge, host e none**. A rede bridge é a padrão, ela funciona como uma ponte virtual, permitindo que todos os contêineres conectados se comuniquem entre si via TCP/IP. Essa rede utiliza o intervalo de endereços IP 172.17.0.0/16, e cada contêiner recebe automaticamente um endereço IP disponível nessa faixa. A comunicação externa é permitida apenas quando as portas são expostas usando o parâmetro `-p` ou `--publish` ao criar o contêiner.

A rede host permite que um contêiner compartilhe diretamente o namespace de rede do host, utilizando a mesma interface de rede e endereço IP do sistema hospedeiro. Isso elimina a sobrecarga de virtualização da rede, sendo útil para aplicações que exigem alta performance. Já a rede none isola completamente o contêiner, não atribuindo nenhuma interface de rede externa, permitindo apenas acesso ao loopback.

Para ambientes mais complexos, é possível criar redes definidas pelo usuário, geralmente com o driver bridge. Essas redes oferecem funcionalidades avançadas, como resolução de nomes automática entre contêineres por meio de um DNS interno do Docker, eliminando a necessidade do uso obsoleto da opção `--link`. Contêineres em redes diferentes não conseguem se comunicar diretamente, a menos que um contêiner esteja conectado a mais de uma rede.

Redes personalizadas podem ser criadas com o comando `docker network create`, e detalhes sobre uma rede específica podem ser inspecionados com `docker network inspect`. O Docker também suporta redes overlay para comunicação entre contêineres em hosts diferentes, utilizando túneis VXLAN, sendo amplamente usado em orquestradores como Docker Swarm.