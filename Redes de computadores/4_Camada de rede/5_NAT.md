
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
3. Ele **anota a origem original** em uma tabela chamada **tabela NAT**.
4. O servidor responde ao IP público.
5. O roteador NAT **olha na tabela** e sabe que deve enviar a resposta para o notebook.
![[Pasted image 20250526193147.png]]

#### 1. NAT Estática (Static NAT)
- **Definição:** Mapeia um único endereço IP privado para um único endereço IP público dedicado. É um mapeamento "um para um" e fixo.
- **Quando usado:** Principalmente para servidores internos que precisam ser acessíveis publicamente com um IP fixo, como um servidor web ou um servidor de e-mail.
- **Exemplo:** Você pode configurar seu roteador para que qualquer tráfego externo para `203.0.113.51` (outro IP público que você possui) seja sempre direcionado para `192.168.1.10` (seu servidor web).
- **Desvantagem:** Não economiza endereços IP públicos, pois requer um IP público para cada IP privado mapeado.

#### 2. NAT Dinâmica (Dynamic NAT)

- **Definição:** Mapeia endereços IP privados para um pool de endereços IP públicos disponíveis. O mapeamento é "um para um", mas o IP público atribuído a um IP privado pode mudar (é dinâmico) a cada nova conexão, dependendo da disponibilidade no pool.
- **Quando usado:** Em cenários onde um grupo de dispositivos internos pode precisar de acesso externo, mas o número de endereços IP públicos disponíveis é menor do que o número total de dispositivos internos.
- **Exemplo:** Se você tiver 50 computadores internos e um pool de 10 IPs públicos, apenas 10 computadores poderão ter acesso externo simultaneamente, cada um usando um IP público diferente do pool.
- **Desvantagem:** Ainda requer um pool de IPs públicos e pode esgotar o pool se muitos dispositivos precisarem de acesso simultâneo.

#### 3. PAT (Port Address Translation) / NAT Sobrecarga (NAT Overload) / NAT com Portas

- **Definição:** Este é o tipo mais comum de NAT, usado na maioria das redes domésticas e pequenas empresas. Ele permite que **vários endereços IP privados compartilhem um único endereço IP público** (ou um pequeno grupo de endereços públicos) **usando diferentes números de porta**.
- **Como funciona:**
    1. **Saída da rede privada:** Quando o computador `192.168.1.10` envia um pacote para a Internet (por exemplo, para um servidor web na porta 80), o roteador NAT intercepta o pacote.
    2. O roteador NAT substitui o endereço IP de origem `192.168.1.10` pelo seu próprio endereço IP público `203.0.113.50`.
    3. Para distinguir entre as conexões de diferentes dispositivos internos que estão usando o mesmo IP público, o roteador NAT também **modifica a porta de origem** do pacote para uma porta de "tradução" única (por exemplo, de `192.168.1.10:12345` para `203.0.113.50:50000`).
    4. O roteador mantém uma **tabela de tradução NAT** que mapeia a combinação IP privado:porta original para o IP público:porta traduzida.
    5. **Retorno da Internet:** Quando o servidor web externo responde, o pacote de retorno chega ao roteador NAT com o endereço de destino `203.0.113.50:50000`.
    6. O roteador NAT consulta sua tabela de tradução, vê que `203.0.113.50:50000` corresponde a `192.168.1.10:12345`, e reescreve o endereço de destino no pacote para `192.168.1.10:12345` antes de encaminhá-lo para o computador correto.
- **Analogia:** É como um prédio de apartamentos com um único carteiro. Cada apartamento tem um número interno, mas toda a correspondência externa é endereçada ao prédio. O carteiro (roteador NAT) sabe qual apartamento recebe qual correspondência com base no número do apartamento e os encaminha corretamente.
- **Vantagens:** A principal vantagem é a **conservação massiva de endereços IPv4**, pois um único IP público pode servir a centenas ou milhares de dispositivos internos. Também oferece o benefício de segurança ao ocultar os endereços internos.
- **Desvantagens:**
    - **Dificulta conexões de entrada:** Serviços externos não podem iniciar uma conexão diretamente para um host interno, a menos que uma regra de **Port Forwarding** (encaminhamento de porta) seja configurada manualmente no roteador. Isso é um problema para jogos online P2P ou servidores internos.
    - **Quebra de alguns protocolos:** Alguns protocolos de rede mais antigos ou específicos que incorporam endereços IP no payload do pacote (e não apenas no cabeçalho) podem não funcionar bem com NAT sem configurações adicionais (como SIP para VoIP).
    - **Rastreamento de usuários:** Dificulta o rastreamento de um usuário específico em logs de IP públicos, já que muitos usuários compartilham o mesmo IP público.

### NAT vs. IPv6

Com a adoção crescente do IPv6, a necessidade de NAT para conservação de endereços é muito menor, pois o IPv6 oferece um espaço de endereçamento praticamente ilimitado. Em um ambiente puramente IPv6, cada dispositivo pode ter seu próprio endereço IP público globalmente roteável, eliminando a necessidade de NAT para esse fim. No entanto, a NAT ainda pode ser usada para propósitos de segurança ou para traduzir entre IPv4 e IPv6 (NAT64/DNS64).

Em resumo, a NAT foi uma solução engenhosa e crucial para a escassez de endereços IPv4, permitindo que a internet continuasse a crescer. Embora tenha suas desvantagens e seja menos necessária com o IPv6, ela continua sendo uma pa