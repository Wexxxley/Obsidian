
---

Os endereços IPv4 são limitados, então **não há endereços públicos suficientes** para todos os dispositivos do mundo. O NAT foi criado como uma solução temporária para esse problema.

O **NAT** (Network Address Translation) é uma técnica usada em redes de computadores que permite que **vários dispositivos em uma rede local compartilhem um único endereço IP público** para se comunicar com a Internet.

A NAT é tipicamente implementada em um roteador ou firewall que atua como um "gateway" entre a rede privada e a rede pública (Internet).

Vamos usar um exemplo simples:
- Sua rede doméstica: `10.0.0/24`
- Seu roteador doméstico tem o IP privado `10.0.0.4` e um IP público `138.76.29.7` (que é o endereço que seu ISP lhe fornece).
- Notebook: 10.0.0.1
- Smartphone: 10.0.0.2
- Console: 10.0.0.3

Quando o notebook acessa um site:
1. Ele envia um pacote para o IP externo do site.
2. O **roteador NAT intercepta** o pacote e substitui o IP de origem por seu **IP público**.
3. Ele **anota o endereço e a porta original** em uma tabela chamada **tabela NAT**.
4. Quando o servidor web externo responde, o pacote de retorno chega ao roteador NAT com o endereço de destino.
5. O roteador NAT **olha na tabela** e sabe que deve enviar a resposta para o notebook.
![[Pasted image 20250526193147.png]]

### NAT vs. IPv6
Com a adoção crescente do IPv6, a necessidade de NAT para conservação de endereços é muito menor, pois o IPv6 oferece um espaço de endereçamento praticamente ilimitado. Em um ambiente puramente IPv6, cada dispositivo pode ter seu próprio endereço IP público globalmente roteável, eliminando a necessidade de NAT para esse fim. No entanto, a NAT ainda pode ser usada para propósitos de segurança ou para traduzir entre IPv4 e IPv6 

