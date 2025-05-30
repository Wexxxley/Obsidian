

---
 O ICMP é usado pelos roteadores para troca de informação de controle da camada de rede. Indicando, por exemplo, que um serviço solicitado não está disponível ou que um host ou roteador não pôde ser alcançado.

**Usado por hosts e roteadores para troca de informação de controle da camada de rede.**

- **Usado por hosts e roteadores:** O ICMP é utilizado tanto por dispositivos finais (como seu computador) quanto por dispositivos intermediários (roteadores) para trocar informações de controle na camada de rede 
- **Error reporting:** Uma das funções primárias do ICMP é relatar erros. Quando algo dá errado com a entrega de um pacote IP o ICMP é usado para enviar uma mensagem de volta ao remetente informando-o sobre o problema.
- **Echo request/reply:** O comando `ping` envia uma mensagem ICMP Echo Request para um host de destino, se o host estiver acessível, ele responde com uma mensagem ICMP Echo Reply. Isso é comumente usado para testar a conectividade da rede e medir o tempo de ida e volta.
- **Transporte de mensagens:** As mensagens ICMP são encapsuladas dentro de datagramas IP. Isso significa que uma mensagem ICMP é a "carga útil" de um pacote IP.

---

### **Tabela de Mensagens ICMP**

| Tipo | Código | Descrição                  | Observações                                             |
| :--- | :----- | :------------------------- | :------------------------------------------------------ |
| 0    | 0      | **Echo Reply**             | Resposta ao comando `ping`.                             |
| 3    | 0      | **Network Unreachable**    | A rede de destino não pode ser alcançada.               |
| 3    | 1      | **Host Unreachable**       | O host de destino não pode ser alcançado.               |
| 3    | 2      | **Protocol Unreachable**   | Protocolo solicitado não disponível no host de destino. |
| 3    | 3      | **Port Unreachable**       | Porta solicitada não disponível no host de destino.     |
| 3    | 6      | **Dest Network Unknown**   | A rede de destino é desconhecida.                       |
| 3    | 7      | **Dest Host Unknown**      | O host de destino é desconhecido.                       |
| 4    | 0      | **Source Quench**          | Indicava congestionamento (pouco usado).                |
| 8    | 0      | **Echo Request**           | Usado pelo `ping` para testar a conectividade.          |
| 9    | 0      | **Router Advertisement**   | Roteadores anunciam sua presença.                       |
| 10   | 0      | **Router Solicitation**    | Hosts solicitam anúncios de roteador.                   |
| 11   | 0      | **TTL Expired in Transit** | O campo TTL do pacote atingiu zero.                     |
| 12   | 0      | **IP Header Bad**          | O cabeçalho IP contém um erro.                          |

---
### **Traceroute e ICMP**
O slide descreve como a ferramenta de rede `traceroute` funciona, utilizando o t (ICMP) para mapear o caminho que os pacotes de dados percorrem através de uma rede até um destino.

Vamos analisar cada ponto:

**Título: Traceroute e ICMP** O título estabelece o tema principal: a relação e o uso do ICMP pela ferramenta `traceroute`.

**1. O transmissor envia uma série de segmentos UDP para o destino**

- Isso descreve o início do processo do `traceroute`. O computador de origem (o transmissor) começa a enviar pacotes de dados.
- O primeiro pacote UDP enviado tem seu campo "Time To Live" (TTL) definido como 1. O TTL é um contador em cada pacote IP que diminui em 1 a cada roteador que o pacote atravessa. Quando o TTL chega a zero, o roteador descarta o pacote.
- **O 2º possui TTL = 2**
    - O segundo pacote UDP enviado tem seu TTL definido como 2.
- **etc.**
    - E assim por diante. Pacotes subsequentes terão TTLs crescentes (3, 4, 5, etc.).
- **nº de porta improvável.**
    - Os pacotes UDP são enviados para um número de porta de destino que é intencionalmente improvável de estar em uso por qualquer serviço legítimo no host de destino (por exemplo, portas muito altas e não registradas). Isso é crucial para o critério de interrupção, como veremos adiante.

**2. Quando o enésimo datagrama chega ao enésimo roteador:**

- Isso se refere ao momento em que um pacote UDP, com um determinado valor de TTL, atinge um roteador específico na rota.
- **O roteador descarta o datagrama.**
    - Como o TTL do pacote atinge zero ao chegar a este roteador (ele decrementa de N para N-1, e então para 0 ao tentar passar por ele), o roteador é obrigado a descartar o datagrama.
- **E envia à origem uma mensagem ICMP (type 11, code 0).**
    - Quando um roteador descarta um pacote devido ao TTL ter expirado, ele gera e envia de volta à origem uma mensagem ICMP do tipo 11, código 0 ("Time Exceeded - TTL expired in transit"). Esta é a chave para o `traceroute` identificar os saltos.
- **A mensagem inclui o nome do roteador e o endereço IP.**
    - A mensagem ICMP "Time Exceeded" normalmente contém informações sobre o roteador que a enviou, incluindo seu endereço IP (e, se disponível, o nome do host via DNS reverso), o que permite ao `traceroute` identificar cada "salto" no caminho.

**3. Quando a mensagem ICMP chega, a origem calcula o RTT.**

- RTT significa "Round-Trip Time" (Tempo de Ida e Volta).
- Ao receber a mensagem ICMP (Tipo 11, Código 0) de um roteador, o computador de origem calcula o tempo que levou desde o envio do pacote UDP original até o recebimento da resposta ICMP. Isso dá uma ideia da latência para aquele salto específico.
- **O traceroute faz isso três vezes.**
    - Para cada salto (cada valor de TTL), o `traceroute` geralmente envia três pacotes UDP. Isso permite calcular a média do RTT e detectar se há inconsistências ou perdas de pacotes em um determinado salto, fornecendo uma visão mais completa da qualidade da conexão.

**4. Critério de interrupção** Este é o mecanismo pelo qual o `traceroute` sabe que chegou ao destino final.

- **O segmento UDP finalmente chega ao hospedeiro de destino.**
    - Isso acontece quando o valor do TTL é grande o suficiente para o pacote UDP chegar até o host final sem expirar no caminho.
- **O destino retorna o pacote ICMP "hospedeiro unreachable" (type 3, code 3).**
    - Lembra que os pacotes UDP foram enviados para um número de porta "improvável"? Quando o pacote UDP chega ao host de destino, o sistema operacional do host tenta entregar o pacote àquela porta. Como não há nenhum aplicativo ouvindo nessa porta, o host de destino gera uma mensagem ICMP do tipo 3, código 3 ("Destination Unreachable - Port Unreachable").
- **Quando a origem obtém esse ICMP, ela para.**
    - Ao receber esta mensagem ICMP específica (Tipo 3, Código 3), o programa `traceroute` na origem sabe que alcançou o host final e, portanto, encerra o processo, pois mapeou todo o caminho.

**Em resumo, a lógica do `traceroute` é a seguinte:**

1. Começa enviando pacotes com TTL baixo (1, depois 2, depois 3, etc.).
2. Cada pacote com TTL baixo "morre" em um roteador sucessivo, fazendo com que esse roteador envie uma mensagem ICMP "TTL Expirado" de volta à origem.
3. A origem usa essas mensagens ICMP para identificar cada roteador no caminho e calcular o tempo de ida e volta para cada um.
4. Quando o pacote finalmente chega ao destino final (porque o TTL é grande o suficiente), o destino responde com uma mensagem ICMP "Porta Inalcançável" (já que nenhuma aplicação está ouvindo na porta improvável).
5. Essa mensagem "Porta Inalcançável" sinaliza ao `traceroute` que ele chegou ao destino, e o processo termina.

Esta é uma técnica engenhosa que permite mapear a topologia da rede entre dois pontos e diagnosticar problemas de conectividade e latência.