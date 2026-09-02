
#Concluded 

---
### **1. DNS (Domain Name System)**

Há duas maneiras de identificar um hospedeiro: 
1. **Nome de hospedeiro**
2. **Endereço IP**
 
As pessoas preferem o nome de hospedeiro e os roteadores preferem endereços IP.<mark style="background: #ADCCFFA6;"> A tarefa principal do DNS é traduzir nomes de hospedeiro para endereços IP. </mark>

O DNS é um **banco de dados** distribuído executado em uma **hierarquia** de servidores de DNS, e um **protocolo de camada de aplicação** que permite que hospedeiros consultem o banco de dados distribuído. O protocolo DNS utiliza UDP. 

> [!EXAMPLE]
> Para que a máquina do usuário possa enviar uma mensagem HTTP ao servidor: www.someschool.edu, ela precisa primeiro obter o endereço IP.
>
> 1. O usuário digita o nome do site no navegador.
> 2. O SO envia uma consulta DNS para um **Servidor DNS** (geralmente fornecido via DHCP pelo seu ISP, ou um público como `8.8.8.8` do Google).
> 3. O servidor DNS responde à consulta com o endereço IP público correspondente.
> 4. Com o IP de destino em mãos, o navegador pode então iniciar a conexão.

---
### **2. Serviços fornecidos pelo DNS**

1. **Resolução de nomes de domínio:** 
    Ex: gaia.cs.umass.edu → 200.17.37.2
    
2. **Mapeamento de apelidos:** Um nome canônico pode ter vários apelidos. 
	Ex: Nome canônico: relay1.west-coast.enterprise.com → Apelido: www.enterprise.com
	
3. **Mapeamento de apelidos para servidores de e-mail:** Direciona e-mails ao servidor correto.
	Ex: empresa.com → mail.empresa.com
	
4. **Balanceamento de carga:** O DNS pode retornar vários endereços IP para um único nome de domínio, alternando a ordem desses IPs para distribuir a carga entre múltiplos servidores.  

 O DNS é dividido em camadas, formando uma **hierarquia**.
 ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf1kCPoUnJMxtbjf7Rl7DQz4SarLgvt-fevAXbitRFqyI__NfNkSoVKCGKF2QBqjDLqYUBBoEiASABPG5439WTUY437KBTDwy21EgEAF7V52258iyiVu8PMwAgg96G1Gqo8-zpJpw?key=HrOhHC0_-ked6RNCpQ0o3PZn)
1. **Servidores raiz:** Sabem onde encontrar os servidores TLDs (.com, .org)
2. **Servidores TLD(Top-Level-Domain):** Sabem onde encontrar os servidores autoritativos.
3. **Servidores autoritativos:** Contêm os registros DNS definitivos.  

**Exemplo**
![400](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc13MwakxHmnjm7iRHQIwIXgrAN-a4C2pNu0AeWsPK3JhfGNRSpAPX_vSRaD7VMpswNIRzCvOFFyX6UbPB9iCxOc35nSa2e4PlHD9hHYUoPkhJDkTihDwf1HczLxFVG20eQ6w898A?key=HrOhHC0_-ked6RNCpQ0o3PZn)  

**Servidor de nomes local:** Sua função é processar a consulta do hospedeiro requisitante.  Por padrão, o Servidor de Nomes Local é definida pelo ISP.

Os ISPs fazem isso para direcionar o tráfego de DNS através de seus próprios servidores de alta velocidade. Isso permite que eles utilizem **cache** resultados de consultas frequentes (como Google, Facebook).

___
### **3. DNS - Protocolo de mensagem**
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeFlyt4CkUZKCo75XcWVH4Ks02zOnnJI46ZXkjTm2IzybuvzELRDs-ifIkRVDYmcbV210mkRzQ98TRhCJazDWJnnfDprOMhLpX0yUlTJZjiV2atu13e6I7YKAWNgB9y5E23kh0i?key=HrOhHC0_-ked6RNCpQ0o3PZn)

  
  
  
  
  
  

