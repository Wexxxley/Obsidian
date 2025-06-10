
#Concluded 

---
### **1. Entendimento**
Os endereços IPv4 são limitados, então **não há endereços públicos suficientes** para todos os dispositivos do mundo. O NAT foi criado como uma solução temporária para esse problema.

O **NAT** (Network Address Translation) é uma técnica que permite que **vários dispositivos em uma rede local compartilhem um único endereço IP público** para se comunicar com a Internet.

A NAT é tipicamente implementada em um roteador que atua como um "gateway" entre a rede privada e a rede pública (Internet).

**Exemplo simples:**
- Sua rede doméstica: `10.0.0/24`
- O roteador tem o IP privado `10.0.0.4` e um IP público `138.76.29.7` (end que o ISP fornece).
- Notebook: 10.0.0.1
- Smartphone: 10.0.0.2
- Console: 10.0.0.3

- Quando o notebook acessa um site:
	1. Ele envia um pacote para o IP externo do site.
	2. O **roteador intercepta** o pacote e substitui o IP de origem por seu **IP público**.
	3. Ele **anota o endereço e a porta original** em uma tabela chamada **tabela NAT**.
	4. Quando o server responde, o pacote chega ao roteador com o endereço nat e a porta nat referente ao processo.
	5. O roteador NAT **olha na tabela** e sabe que deve enviar a resposta para o notebook.
![[Pasted image 20250526193147.png]]

- Quando seu roteador usa NAT, ele pode atribuir uma porta _diferente_ para cada conexão _simultânea_ que sai da sua rede privada. 
- Por exemplo, o Notebook na sua rede abre uma conexão usando a porta de origem 50000 e o Celular abre outra conexão usando a porta de origem 50001, o roteador NAT pode traduzir ambas para o mesmo IP público mas usando portas traduzidas distintas.
- Ex: Notebook para`138.76.29.7:10001` e Celular para `138.76.29.7:10002`.

Na teoria, um único IP público com NAT pode suportar até 65.535 conexões _simultâneas de saída_ para **cada protocolo** (TCP ou UDP).  Na prática, o limite é menor devido a recursos do roteador.

![[Pasted image 20250610101815.png]]
- **IP origem:** O endereço do computador que iniciou a conexão na rede local. ``Ex: 10.0.0.1``
- **Porta origem:** A porta que o computador de origem usou para iniciar a conexão. Ex: `50000`.
- **IP nat:** O endereço IP público que o roteador está usando. Ex: ``138.76.29.7``
- **Porta nat:** A porta que o roteador atribuiu para essa conexão específica. O roteador "mapeia" a porta de origem interna para esta porta externa. Ex: `10000`.
- **IP server:** O endereço público do servidor. Ex: `172.217.160.142` 
- **Porta server:** A porta do serviço no servidor externo para o qual a conexão é destinada. Ex: `80`
- **Data/hora do recebimento:** Data e hora em que a entrada na tabela NAT foi criada ou a última vez que o tráfego correspondente foi visto.
- **Protocolo:** O protocolo da Camada de transporte que está sendo usado para a conexão.

### Exemplo de Comun

---
### **1.2 NAT é Controverso**
Apesar de sua utilidade e de ter "salvado" o IPv4, a NAT é frequentemente criticada por ir contra princípios fundamentais do design da Internet.
1. **Número de Porta Deveria Identificar Processo e Não Hospedeiro:** A ideia de um número de porta é identificar uma **aplicação específia** de um host, não o host em si. 

2. **Roteadores Deveriam Processar Somente Até a Camada 3:** O modelo TCP/IP estabelece que roteadores operam na camada de rede somente. A NAT, particularmente **inspeciona e modifica os números de porta**, o que é informação da Camada 4. Isso faz com que o roteador NAT aja como um "proxy".

3. **Violação do Argumento Fim-a-Fim:** Esse princípio afirma que a complexidade de uma rede devem estar nas **extremidades (hosts)**, e a rede em si (roteadores) deve ser o mais simples possível. A NAT **modifica os cabeçalhos dos pacotes** (endereços IP e portas). Isso impede que os hosts finais se comuniquem "diretamente" de ponta a ponta.
    
4. **NAT e aplicações P2P:** Aplicações como torrents e alguns jogos online dependem de que os "peers" possam se conectar diretamente uns aos outros. Com a NAT, os hosts internos estão "escondidos" atrás do IP público do roteador. Para que essas aplicações funcionem, muitas vezes são necessárias técnicas adicionais
    - Isso impõe uma carga extra aos desenvolvedores de software, que precisam projetar suas aplicações para lidar com o ambiente NAT.

5. **NAT vs. IPv6:** Com a adoção crescente do IPv6, a necessidade de NAT para conservação de endereços é muito menor, pois o IPv6 oferece um espaço de endereçamento praticamente ilimitado. Em um ambiente puramente IPv6, cada dispositivo pode ter seu próprio endereço IP público globalmente roteável, eliminando a necessidade de NAT para esse fim. No entanto, a NAT ainda pode ser usada para propósitos de segurança ou para traduzir entre IPv4 e IPv6 