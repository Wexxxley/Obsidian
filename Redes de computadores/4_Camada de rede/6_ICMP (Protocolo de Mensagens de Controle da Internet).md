

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

O comando `traceroute` é uma ferramenta de diagnóstico de rede usada para **rastrear a rota que os pacotes percorrem de um computador de origem até um destino específico**

**1. O transmissor envia uma série de segmentos UDP para o destino**
- Isso descreve o início do processo do `traceroute`. O computador de origem (o transmissor) começa a enviar pacotes de dados.
- O primeiro pacote UDP enviado tem seu campo TTL definido como 1. O segundo pacote UDP enviado tem seu TTL definido como 2 e assim por diante
- Os pacotes UDP são enviados para um número de porta de destino que é intencionalmente improvável de estar em uso. Isso é crucial para o critério de interrupção.

**2. Quando o enésimo datagrama chega ao enésimo roteador:**
- Como o TTL do pacote atinge zero, o roteador é obrigado a descartar o datagrama.
- Quando um roteador descarta um pacote devido ao TTL ter expirado, ele gera e envia de volta à origem a mensagem "TTL expired in transit". A mensagem ICMP contém informações sobre o roteador que a enviou, o que permite ao `traceroute` identificar cada "salto" no caminho.

**3. Quando a mensagem ICMP chega, a origem calcula o RTT.**
- RTT significa "Round-Trip Time" (Tempo de Ida e Volta).
- Para cada salto, o `traceroute` geralmente envia três pacotes UDP. Isso permite calcular a média do RTT e detectar se há inconsistências.

**Em resumo, a lógica do `traceroute` é a seguinte:**

1. O transmissor envia uma série de segmentos UDP com TTL 1, 2, 3 e assim sucessivamente. Os pacotes são enviados para um número de porta de destino que é improvável de estar em uso. Isso é crucial para a interrupção.
2. Cada pacote com TTL baixo "morre" em um roteador, fazendo com que esse roteador envie uma mensagem ICMP "TTL Expirado" de volta à origem. A mensagem ICMP contém informações sobre o roteador que a enviou, o que permite ao `traceroute` identificar cada "salto" no caminho.
3. A origem usa essas mensagens ICMP para identificar cada roteador no caminho e calcular o RTT (Round Trip Time), ou seja, o tempo de ida e volta para cada um.
4. Quando o pacote finalmente chega ao destino final. o destino responde com uma mensagem ICMP "Porta Inalcançável" (já que nenhuma aplicação está ouvindo na porta improvável).
5. Essa mensagem "Porta Inalcançável" sinaliza ao `traceroute` que ele chegou ao destino, e o processo termina.

Esta é uma técnica engenhosa que permite mapear a topologia da rede entre dois pontos e diagnosticar problemas de conectividade e latência.