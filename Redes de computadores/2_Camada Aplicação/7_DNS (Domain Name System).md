
---
# 1 DNS (Domain Name System)

Há duas maneiras de identificar um hospedeiro: por um ==nome de hospedeiro== e por um ==endereço IP.== As pessoas preferem o identificador nome de hospedeiro, ao passo que roteadores preferem endereços IP. Para conciliar essas preferências, é necessário um serviço que traduza nomes de hospedeiro para endereços IP. Esta é a tarefa principal do DNS (domain name system) 

O DNS ==é um banco de dados== distribuído executado em uma hierarquia de servidores de DNS, e ==um protocolo de camada de aplicação== que permite que hospedeiros consultem o banco de dados distribuído. O protocolo DNS utiliza UDP. O DNS costuma ser empregado por outras entidades da camada de aplicação — inclusive HTTP, SMTP e FTP.

Exemplo, Para que a máquina do usuário possa enviar uma mensagem HTTP ao servidor: www.someschool.edu, ela precisa primeiro obter o endereço IP. Isso é feito da seguinte maneira: 
1. A própria máquina do usuário executa o lado cliente da aplicação DNS. 
2. O navegador extrai o nome de hospedeiro, www.someschool.edu, do URL e passa o nome para o lado cliente da aplicação DNS. 
3. O cliente DNS envia uma consulta contendo o nome do hospedeiro para um servidor DNS. 
4. O cliente DNS por fim recebe uma resposta, que inclui o endereço IP correspondente ao nome de hospedeiro. 
5. Tão logo o navegador receba o endereço do DNS, pode abrir uma conexão TCP com o processo servidor HTTP localizado na porta 80 naquele endereço IP.
  
---
# 2. Serviços fornecidos pelo DNS

1. **Resolução de nomes de domínio:** Tradução de nomes legíveis para endereços IP.  
    Ex: gaia.cs.umass.edu → 200.17.37.2
2. **Mapeamento de apelidos:** Um nome canônico pode ter vários apelidos. Ex: 
	- Nome canônico: relay1.west-coast.enterprise.com
	- Apelidos: www.enterprise.com, enterprise.com
3. **Mapeamento de apelidos para servidores de e-mail:** Direciona e-mails ao servidor correto. Ex: empresa.com → mail.empresa.com
4. **Balanceamento de carga:** O DNS pode retornar vários endereços IP para um único nome de domínio, alternando a ordem desses IPs para distribuir a carga entre múltiplos servidores.  

Base de dados distribuída e hierárquica:  O DNS é dividido em camadas, formando uma hierarquia.![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf1kCPoUnJMxtbjf7Rl7DQz4SarLgvt-fevAXbitRFqyI__NfNkSoVKCGKF2QBqjDLqYUBBoEiASABPG5439WTUY437KBTDwy21EgEAF7V52258iyiVu8PMwAgg96G1Gqo8-zpJpw?key=HrOhHC0_-ked6RNCpQ0o3PZn)
1. **Servidores raiz:** Sabem onde encontrar os servidores TLDs (.com, .org)
2. **Servidores TLD(Top-Level-Domain):** Sabem onde encontrar os servidores autoritativos para domínios (ex: google.com)
3. **Servidores autoritativos:** Contêm os registros DNS definitivos.  
  
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc13MwakxHmnjm7iRHQIwIXgrAN-a4C2pNu0AeWsPK3JhfGNRSpAPX_vSRaD7VMpswNIRzCvOFFyX6UbPB9iCxOc35nSa2e4PlHD9hHYUoPkhJDkTihDwf1HczLxFVG20eQ6w898A?key=HrOhHC0_-ked6RNCpQ0o3PZn)  

 Atualmente existem 13 DNS raiz no mundo. Cada um desses 13 representa uma rede de servidores espalhados pelo mundo. Vários servidores físicos em diferentes localizações compartilham o mesmo endereço IP. O roteamento faz com que o cliente seja conectado ao servidor mais próximo.  Embora existam 13 identificadores principais, o número total de instâncias físicas ultrapassa os 1600.

**Servidor de nomes**
 Um servidor de nomes local é o servidor de DNS que fica mais próximo do usuário final, geralmente mantido pelo provedor de internet. Quando você digita um endereço no navegador, seu computador não sabe de imediato o IP desse site. Ele envia a consulta ao servidor de nomes local.
 
---
# **3.Registros de recursos(RR)**
Os servidores DNS armazenam registros de recursos (RR) que fornecem mapeamentos de nomes de hospedeiros para endereços IP. Cada mensagem de resposta DNS carrega um ou mais registros de recursos. 

Um registro de recurso é uma tupla de  que contém os seguintes campos: ==(Name, Value, Type, TTL)==

**TTL** é o tempo de vida útil do registro de recurso; determina quando um recurso deve ser removido de um cache. 

1. **Type A**: recebe o nome canônico e retorna o ipv4
2. **Type AAAA:** recebe o nome canônico e retorna o ipv6
3. **Type NS**: Recebe um domínio e retorna o nome de um servidor DNS autoritativo.
4. **Type CNAME**: Recebe um apelido e retorna o nome canônico.
5. **Type MX**:  Recebe o domínio e retorna o nome canônico do server de email 
6. **PTR**: recebe um ipv4/ipv6 e retorna o nome canônico. Aconsulta precisa ser explicita.

___
# 4 **DNS - Protocolo de mensagem**

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeFlyt4CkUZKCo75XcWVH4Ks02zOnnJI46ZXkjTm2IzybuvzELRDs-ifIkRVDYmcbV210mkRzQ98TRhCJazDWJnnfDprOMhLpX0yUlTJZjiV2atu13e6I7YKAWNgB9y5E23kh0i?key=HrOhHC0_-ked6RNCpQ0o3PZn)
  
  
  
  
  
  