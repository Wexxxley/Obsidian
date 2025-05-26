
---

Os endereços IPv4 são limitados, então **não há endereços públicos suficientes** para todos os dispositivos do mundo. O NAT foi criado como uma solução temporária para esse problema.


O **NAT** (Network Address Translation) é uma técnica usada em redes de computadores que permite que **vários dispositivos em uma rede local compartilhem um único endereço IP público** para se comunicar com a Internet.

Imagine uma rede doméstica com os seguintes dispositivos:
- Notebook: 10.0.0.1
- Smartphone: 10.0.0.2
- Console: 10.0.0.3
- Roteador (com NAT): IP interno 10.0.0.4, IP externo 138.76.29.7

Quando o notebook acessa um site:
1. Ele envia um pacote para o IP externo do site.
2. O **roteador NAT intercepta** o pacote e substitui o IP de origem por seu **IP público**.
3. Ele **anota a origem original** em uma tabela chamada **tabela NAT**.
4. O servidor responde ao IP público.
5. O roteador NAT **olha na tabela** e sabe que deve enviar a resposta para o notebook.
![[Pasted image 20250526193147.png]]




